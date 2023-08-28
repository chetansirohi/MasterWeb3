### You have been tasked with developing a smart contract for a new token on the Ethereum network. The contract should allow for the transfer of tokens between authorizedUsers, with the ability to add or remove authorizedUsers from the system.

```
The token contract should have the following features:

  A mapping that stores the token balance of each user in the system called balances.
  An array to store the addresses of authorizedUsers.
  A constructor that adds the creator of the contract as an authorized user.
  A modifier that ensures only authorizedUsers can access certain functions.
  A function to transfer tokens between users that can only be accessed by authorizedUsers and checks if the sender has sufficient balance.
  A function to add new authorizedUsers that can only be accessed by authorizedUsers.
  A function to retrieve the list of authorizedUsers.
  You should ensure that the contract is secure and handles errors gracefully, with appropriate error messages displayed when necessary.

Constraints:

  You must make sure you maintian a mapping between each `authorizedUser` and their amounts called `balances`

Hints

  Who will be the first `authorizedUser` on the contract?
  What is the keyword to throw an error message if a condition isn't met?
```

### Solution

```
pragma solidity ^0.8.0;

contract Token {
    mapping(address => uint256) public balances;
    address[] authorizedUsers;

    constructor() {
        // How will we get the first authorized user?
      authorizedUsers.push(msg.sender);
    }

    modifier onlyAuthorized() {
        bool isAuthorized = false;
        // TODO
        for(uint256 i =0; i<authorizedUsers.length;i++){
          if(authorizedUsers[i] == msg.sender){
            isAuthorized=true;
            break;
          }
        }
        require(isAuthorized, "Unauthorized access");
        _;
    }

    function transfer(address recipient, uint256 amount) public onlyAuthorized {
        // TODO
        require(balances[msg.sender] >= amount, "Insufficient balance");
        balances[msg.sender] -= amount;
        balances[recipient] += amount;

    }

    function addAuthorizedUser(address user) public onlyAuthorized {
        // TODO
        authorizedUsers.push(user);
    }

    function getAuthorizedUsers() public view returns (address[] memory) {
        // TODO
        return authorizedUsers;
    }
}
```
