# Writing Gas Optimized Smart Contracts
Gas-efficient code is the mark of an adept Solidity developer. Although writing in Solidity is designed to be a simple process, writing optimized contracts requires deep knowledge of the language and the EVM. And this can only be attained through deliberate study.

The ways to minimize gas consumption fall under one of two categories:

Runtime cost optimization. These optimizations minimize the cost of executing functions in the contract.
Deployment cost optimization. These optimizations minimize the size of a contract, and hence, the cost of deploying it.
Runtime Cost Optimization
Compiling Solidity code produces bytecode. Bytecode is essentially a sequence of EVM instructions, each incurring a set amount of gas. The optimizations below involve tweaking Solidity code such that the resultant bytecode consumes less gas when executed.

Reducing Storage Access
Among the different instructions in the EVM, those that read and write onto a contract’s storage are the most expensive. Consequently, writing code that minimizes these costs will save significant gas.

Typically, if you find yourself accessing a storage variable multiple times, you could see appreciable savings by caching its value into memory.
```
uint256 public stateVariable;

function unoptimized(uint256 iterations) public {;
    for (uint256 i; i < iterations; i++) {
        // Read and write from stateVariable 
    }
}

function optimized(uint256 iterations) public {
    uint256 cache = stateVariable;
    for (uint256 i; i < iterations; i++) {
        // Read and write from cache
    }
		stateVariable = cache;
} 

```
Functions unoptimized() and optimized() both achieve the same outcome. But unoptimized can demand a frightful number of storage reads and writes, while optimized requires only a single read, along with a single write.
Packing Variables
Similar to memory, storage in the EVM is also segmented into 256-bit slots. Consider the following contracts:
```
contract nonPackedContract {

    uint256 a; // └─ Slot 0
    uint256 b; // └─ Slot 1

    // Rest of contract...
}

contract packedContract {

    uint128 a; // ┐
    uint128 b; // ┴─ Slot 0
    
    // Rest of contract...
} 

```
nonPackedContract will require two 256-bit storage slots. packedContract, on the other hand, will pack a and b into a single storage slot. Does this mean, ignoring overflow, the latter is more gas efficient? Despite many online resources claiming so, this might not always be true…
First, let us see the benefit of packing variables. Consider how nonPackedContract can be implemented.

```
contract nonPackedContract {

    uint256 a; // └─ Slot 0
    uint256 b; // └─ Slot 1

    function readSum() public view returns (uint256) {
        return a + b;
    }

}
```
Feeding the above Solidity code into the optimizer might result in the following sequence of instructions for readSum().
* Read storage slot #0 for a.
* Read storage slot #1 for b.
* Sum the values and return the result.

All in all, readSum() requires reading from 2 storage slots.
Now, consider the alternative where packedContract is used.

```
contract packedContract {

    uint128 a; // ┐
    uint128 b; // ┴─ Slot 0

    function readSum() public view returns (uint128) {
        return a + b;
    }

} 
```
The optimizer will likely transform readSum() into the following sequence of instructions:
* Cache storage slot #0 into memory.
* Unpack the cached value to read a.
* Unpack the cached value to read b.
* Sum the two unpacked values and return the result.
Now, packedContract.readSum() only requires a single storage read, 1 less than nonPackedContract.readSum(). Although unpacking the slot to read a and b incurs costs, these are not as expensive. Hence, packedContract is more efficient than nonPackedContract.
Next, let us consider a scenario where the converse is true. Consider this implementation of the 2 contracts.

```
contract nonPackedContract {

    uint256 a; // └─ Slot 0
    uint256 b; // └─ Slot 1

    function readA() public view returns (uint256) {
        return a;
    }

}

contract packedContract {

    uint128 a; // ┐
    uint128 b; // ┴─ Slot 0

    function readA() public view returns (uint128) {
        return a;
    }

}

```

Think about what the compiled bytecode for each contract might look like. Both will demand a single storage read. However, on top of that, packedContract.readA() will require additional gas to unpack the slot’s value to read a. Thus, packedContract is actually the less prudent choice!
Generally, it is only wise to pack your variables into the same slot if they are typically accessed together. We have to bear in mind that using types smaller than 256 bits (e.g. uint128) incurs overhead since the EVM needs to add additional instructions to convert 256-bit words into these smaller types. If we rarely or never access storage variables together, then this overhead can turn out to be more costly than the gains provided by packing.
Cleaning Up State
Contracts can selfdestruct(), and a contract’s storage can be cleared by setting any non-zero slot back to 0. Both operations downsize the global blockchain state by a little.
It is commonly accepted that one can refund gas when they perform either of these two actions, and this was true for a while, in hopes of incentivizing good state hygiene in the blockchain.

However, after the EVM's London hard fork, this is no longer always true. Before the fork, gas refunds were economically problematic. They gave rise to gas tokens which artificially increased the blockchain’s state size. They also resulted in blocks with sizes far larger than their stated gas limit. As a result, EIP-3529 was introduced and integrated, which led to:
* The removal of refunds from selfdestruct().
* And the reduction of refunds when clearing a contract’s storage.
The rationale behind EIP-3529 and the changes it introduces are interesting. Do give the document a read!
What does this mean for smart contract optimization?

Firstly, unlike before, there is no longer any gas incentive to selfdestruct() contracts. Secondly, operations that clear storage, like delete, may not always result in net gas saved. For instance, let us consider the following example.
```
contract KittenVault {

    mapping(uint256 => address) kittenOwner;
    mapping(uint256 => string) kittenName;
	
    // ...
	
    function burnKitten(uint256 id) {
        delete kittenOwner[id]; // Step 1
        delete kittenName[id]; // Step 2
    }

    function burnKitten2(uint256 id) {
        delete kittenOwner[id]; // Step 1
        // We leave kittenName intact.
    }

}
```
EIP-3529 asserts the following truth: the gas refund from clearing a storage slot will be less than the gas required to access the storage slot in the first place. We break down the second step of burnKitten() into the following EVM operations:
Access the storage slot holding kittenName[id]. This costs 
 X
 gas.
Delete the storage slot. This refunds 
Y
 gas.
EIP-3529 ensures that 
�
>
�
 ! This means the second step of burnKitten() does not result in net gas refund, and burnKitten2() is cheaper than burnKitten().
This does not mean that delete never saves gas. In scenarios where storage access is inevitable, clearing storage is still profitable.

```
contract catVault {

    mapping(uint256 => address) kittenOwner;
    mapping(uint256 => string) kittenName;

    mapping(uint256 => address) catOwner;
    mapping(uint256 => string) catName;
	
    // ...
	
    function evolveKitten(uint256 id) {
        catOwner[id] = kittenOwner[id];
        catName[id] = kittenName[id]; // Accessing storage incurs X gas
        delete kittenOwner[id];
        delete kittenName[id]; // Deleting storage refunds Y gas
    }

    function evolveKitten2(uint256 id) {
        catOwner[id] = kittenOwner[id];
        catName[id] = kittenName[id]; // Accessing storage incurs X gas
        delete kittenOwner[id];
    }

}
```
In this scenario, evolveKitten() costs less than evolveKitten2()! Both functions have already invested gas in accessing the storage slot containing kittenName[id], but only evolveKitten() enjoys a gas refund.
The bottom line is that clearing a storage slot is only profitable if the function already needs to access the storage slot at least once.

Hardcoding State Variables
State variables that are labeled constant and immutable are not stored in storage. Instead, they are embedded into a contract's bytecode. These variables can be read for just a fraction of the gas price since no storage read is required.
Both variables are read-only and cannot be mutated upon initialization. immutable state variables can be initialized in the contract's constructor but constant variables must be declared as literals.
```
contract myContract {

    uint256 constant a = 100; // Declared as literal
    uint256 immutable b; // Initialized in constructor

    constructor(uint256 _b) {
        b = _b;
    }
}
```
One restriction regarding immutable variables is that you cannot use them inside a pure function, you can find a full discussion on why here.
Calldata or Memory Parameters
Calldata is a cheap read-only data location that stores the arguments of function calls.

For external functions, when dynamic parameters (arrays, strings and structs) are labeled as memory, they will be copied from calldata to memory, and will become more costly to access. In contrast, calldata parameters point directly to the calldata location, and are cheaper to use.
Hence, if dynamic parameters need not be mutated, it is best to keep them labeled as calldata.
Unchecked Arithmetic
Since Solidity 0.8.0, all arithmetic operations check for integer overflow and underflow.
Naturally, these checks involve additional instructions which cost gas. In cases where it is safe to assume overflow is impossible, these checks will unnecessarily incur gas.

Take the simple case of iterating over a finite number of items:

```
function iterate(int64[] calldata _array) public view {
    for (int256 i; i < array.length; i++) {
        // Do something...
    }
}
```
We know that array will never be as large as 2^256, and i will not overflow. However, the i++ operation checks for overflow in each iteration, and will wastefully spend gas.
To manually disable overflow checks, we can use the unchecked keyword and rewrite iterate like so:
```
function iterate(int64[] calldata array) public view {
    for (int256 i; i < array.length;) {
        // Do something...

        unchecked {
            i = i + 1;
        }
    }
}
```
Arithmetic Tricks
For certain arithmetic operations, bitwise operators can serve as gas-efficient alternatives. For instance:

* Multiplication by a power of 2
* Division by a power of 2
Not accounting for overflow, these 2 operations achieve the same effect.
```
variable << 1;
variable * 2'
```
Keep in mind that by not using arithmetic operators you are no longer protected by built-in overflow checks.

Consider how bit shifts can be extended to support multiplications and division by other powers of 2!

Inline Assembly
In some specific cases, directly using inline assembly is the only way to further optimize a snippet of code. If you are unfamiliar with inline assembly, visit our Learning Assembly campaign!
Other Quirks
There are many other lesser-known gas-saving tricks in Solidity. Although some of them yield minuscule results, it is still cool to know them! Here are just a few:

* >= is slightly cheaper than >.
* Using 2 require statements is cheaper than using only 1 with &&.
* Writing on a used storage slot is cheaper than writing on a new one.
* The order and names of external functions do influence their gas cost! In general, functions declared earlier are cheaper to call.
++i is slightly cheaper than i++ and i = i + 1 because it directly writes onto the i variable (rather than making a copy).
* Deployment Cost Optimization
* Deployment of contracts incurs an appreciable amount of gas as well. The larger the contract's bytecode, the more expensive the deployment. Hence, it might be worthwhile to consider minimizing the size of a smart contract.

This is especially important for applications that require users to deploy their own contracts.

Internal Functions
The use of internal and private functions can eliminate duplicate code, and significantly downsize contracts.

```
contract myContract {

    function foo() external {
        _commonFunction();
        // Do something...
    }
	
    function bar() external {
        _commonFunction();
        // Do something else...
    }
	
    function _commonFunction() internal {
        // Do something common...
    }

}
```
How about when the internal or private function is only called once? Will the bytecode overhead required to store the code as an independent function result in an overall increase in contract size?

```
contract myOtherContract {

    function foo() external {
        _commonFunction();
        // Do something...
    }
	
    function _commonFunction() internal {
        // Do something else...
    }

}
```
Theoretically, yes. But when you compile with the Solidity optimizer, the optimizer will likely embed the inner function’s code directly into the calling function. Hence, this is typically not something you should worry about!

Modifier Wrappers
When functions use modifiers, the Solidity compiler embeds a copy of the modifier’s code into each of these functions. If the modifier is heavy, or used often, multiple copies of it will result in a substantial increase in bytecode size.

```
modifier myExpensiveModifier() {
    // do something gas expensive
    _;
}

function aFunction() public view myExpensiveModifier() {
    // ...
}
```
```
The use of private/internal functions can alleviate this problem.
modifier myExpensiveModifier() {
    _myExpensiveModifier();
    _;
}

function _myExpensiveModifier() internal view {
    // do something gas expensive
}

function aFunction() public view myExpensiveModifier() {
    // ...
}
```
This way, only the call to _myExpensiveModifier is embedded in every modified function, rather than the whole logic.
Custom Errors
Since Solidity 0.8.4 you can use custom errors instead of revert strings. This can downsize contracts as errors are encoded as 4 byte selectors, rather than whole strings.
Take the 2 examples below.
```
contract A {

    function isAuthorized() public {
        if (msg.sender != owner) {
            revert "Unauthorized";
        }
    }

}

contract B {

    // Define a custom error
    error unauthorizedError();
	
    function isAuthorized() public {
        if (msg.sender != owner) {
            revert unauthorizedError();
        }
    }
	
}
```
Assuming both functions revert, contract B is smaller than contract A since the revert data is only 4 bytes long. The encoded error would be the first 4 bytes of keccak256("unauthorizedError()"), and there will be no loss of clarity since the error signature itself can be inferred from the ABI of the contract.
/// The contract ABI will contain the error signature.
```
{
    "inputs": [],
    "name": "unauthorizedError",
    "type": "error"
}
```
Custom errors can also result in less gas spent when the function reverts, since the logged data might be shorter than the original string literal.

We can also add parameters to errors, just like in functions. Take the following example.

```
/**
 * @notice thrown when attempting to transfer more tokens than msg.sender currently have
 * @param amount the amount requested for the transfer
 * @param balance the current balance of msg.sender
 */
error insufficientBalance(uint256 amount, uint256 balance);
```
The error would be encoded using the first 4 bytes of keccak256("insufficientBalance(uint256, uint256)") followed by amount and balance abi-encoded. This feature allows runtime error messages.
Using Constructors
Since constructors are only run once, they are not included in a contract’s deployed bytecode. Thus, if possible, pushing pre-computation into a contract’s constructor can reduce the cost required to deploy it.

Other Methods
There are many other methods of downsizing contracts that achieve greater results. However, they require an architectural overhaul, and might not fall under the category of minor “optimizations”. Some other ways:

Use of minimal proxies
Use of libraries
The Cost of Optimization
Contract optimization is a double-edged sword. More often than not, optimizations result in less readable code. In turn, less readable code results in a codebase that is difficult to maintain, and contracts that are more prone to bugs.

Extreme smart contract optimization can serve as practice and an opportunity for developers to flex their understanding of Solidity and the EVM. However, in practice, optimization should be recognized as a balancing act. The few cents you save on transactions might not be worth the millions you lose to that devious bug.
