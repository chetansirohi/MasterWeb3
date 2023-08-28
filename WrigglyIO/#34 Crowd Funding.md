### Create a Solidity contract called Crowdfunding that allows users to donate funds to a project and tracks the total amount raised. Ensure that only the owner can withdrawFunds

```
Example 1:

  Input: 1500000000000000000
  Output: 1500000000000000000
  Explanation: 1.5 ether is donated and total raised is set to 1500000000000000000 wei.
  
Constraints:

The value will be passed through the msg and therefore does not need to be passed to `donate`.

Hints

  Set the contract creator as the owner in the constructor.
  Update the donate() function to update the totalRaised variable with the amount of ether donated.
  Allow the owner to withdraw the entire balance of the contract in the withdrawFunds() function.

```

### Solution

```
pragma solidity ^0.8.4;

contract Crowdfunding {
    address public owner;
    uint public totalRaised;

    constructor() {
        // TODO: set the contract creator as the owner
        owner = msg.sender;
    }

    function getOwner() public view returns (address) {
        // TODO
        return owner;
    }

    function donate() public payable {
        // TODO: update the totalRaised variable with the amount of ether donated
        require(msg.value > 0, "Please enter an amount greater than zero.");
        totalRaised += msg.value;

    }

    function getTotalRaised() public view returns (uint) {
        return totalRaised;
    }

    function withdrawFunds() public restricted {
        // TODO: allow the owner to withdraw the entire balance of the contract
        require(totalRaised > 0, "There are no funds to withdraw.");
        uint amtPayable = totalRaised;
        totalRaised =0;
        payable(owner).transfer(amtPayable);
        
    }

    modifier restricted() {
        require(msg.sender == owner, "Only the owner can call this function.");
        _;
    }
}

```
