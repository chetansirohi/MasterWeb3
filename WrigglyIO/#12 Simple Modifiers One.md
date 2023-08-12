In Solidity, the things that go after the method names are called "function modifiers" or "keywords". These are special keywords that are used to modify the behavior of a function or specify additional properties about it.

Here are some common function modifiers in Solidity:
```
public : This modifier makes the function accessible from outside the contract. It generates a public getter function that can be used to retrieve the value of any public state variable.

private : This modifier makes the function only accessible from within the contract. It cannot be called from outside the contract or inherited contracts.

external: This modifier is used for functions that are meant to be called from outside the contract. It saves gas by not creating a context for the function call.

internal: This modifier makes the function accessible only from within the contract and any contracts that inherit from it. It cannot be called from outside the contract hierarchy.
```
In addition to these modifiers, there are other modifiers that can be used to specify the function's visibility, state mutability, and other properties. For example, the view modifier is used to indicate that the function does not modify the contract's state, and the payable modifier is used to indicate that the function can receive Ether as part of the transaction.

Modifiers can be combined by placing them in a specific order before the function declaration. For example, a function can be declared as public view returns (uint256) to indicate that it is a public function that does not modify the state of the contract and returns a uint256 value.

```
Constraints:

  return from the public view of the contract instance
  you cannot access public variables in the `pure` method

Hints

  public `view` methods are public and can read the state of the contract, but not modify any of it
  public pure` methods are public but cannot read or write to any of the state in the contract
```

### Solution

```
pragma solidity ^0.8.0;

contract SimpleHash {
    uint256 public value;

    function incrementValue() public {
        // TODO
      value++;
    }

    function getValue() public view returns (uint256) {
        // TODO
      return value;
    }

    function addNums(uint256 a, uint256 b) public pure returns (uint256) {
        // TODO
      return a + b ;
    }
}
```
