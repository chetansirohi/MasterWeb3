You are tasked with writing a smart contract that allows the owner of the contract to set a number and retrieve it. The contract should have a custom modifier that ensures only the contract owner can call the setNumber function. Additionally, the getNumber function should only be accessible within the contract itself.

To accomplish this, you can create a new contract called MyContract with two public state variables: owner of type address, and myNumber of type uint. In the constructor, set the owner variable to msg.sender, which is the address of the account that deploys the contract.

Next, create a custom modifier called onlyOwner that checks if the caller of a function is the same as the owner of the contract. If not, the function should revert with the message "Only the contract owner can call this function".

Then, create a function called setNumber that takes a uint256 parameter and is marked as external and onlyOwner. Inside the function, set the value of myNumber to the input parameter.

Finally, create a function called getNumber that is marked as internal and returns the value of myNumber. Since it is marked as internal, it can only be called from within the contract itself.

By implementing this contract, you will demonstrate how to use custom modifiers to control access to functions and state variables within a smart contract.


```
Constraints:

  You must make sure only the owner of the contract can alter the number

Hints
  Revert if the sender is not the owner of the contract

```

### Solution

```
pragma solidity ^0.8.0;

contract SimpleModifiersThree {
    address public owner;
    uint256 public myNumber;

    constructor() {
        // TODO
      owner = msg.sender;
    }

    modifier onlyOwner() {
        // TODO
      require(msg.sender == owner);
        _;
    }

    function setNumber(uint256 _number) external onlyOwner {
        // TODO
      myNumber = _number;
    }

    function getNumber() external view returns (uint256) {
        // TODO
      return  myNumber;
    }
}
```
