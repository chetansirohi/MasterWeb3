### You are tasked with implementing a smart contract that allows users to register their personal information, including their name and email address. The contract should store this information permanently on the blockchain and allow users to retrieve their own information at any time.

```
Example 1:

  Input: ["Sidd", "Sidd@gmail.com"]
  Output: ("Sidd", "Sidd@gmail.com")
  Explanation: getTeamPlayers() would only contain jersey number 0 with the address 0x123

Constraints:

  The function should emit an event when ether is transferred.

Hints
  registerUser() - Add the user's info to the userMapping
  getUserInfo() - Return's the user's info from userMapping
  updateUserInfo() - Use userMapping to update the user's info
  deleteUser() - Deletes the user's info from userMapping

```

### Solution

```
pragma solidity ^0.8.4;

contract UserRegistration {
    
    // Define a struct to hold user information
    struct UserInfo {
        string name;
        string email;
    }
    
    // Define a mapping to store user information
    mapping(address => UserInfo) private userMapping;
    
    // Define an event to emit when a new user is registered
    event NewUserRegistered(address indexed userAddress, string name, string email);

    // Define the contract owner
    address public owner;
    
    // Constructor to set the contract owner
    constructor() {
        owner = msg.sender;
    }

    // Define a modifier to restrict certain functions to the owner of the contract
    modifier onlyOwner() {
        require(msg.sender == owner, "Caller is not the owner");
        _;
    }
    
    // Define a function to register user information
    function registerUser(string memory _name, string memory _email) public {
        // TODO: Store user information in the mapping
        userMapping[msg.sender] = UserInfo(_name,_email);
        emit NewUserRegistered(msg.sender, _name, _email);
        
        // TODO: Emit event to notify that a new user is registered
    }
    
    // Define a function to retrieve user information
    function getUserInfo() public view returns(string memory name, string memory email) {
        // TODO: Retrieve user information from the mapping
        return (userMapping[msg.sender].name,userMapping[msg.sender].email);
        // TODO: Return user information
    }
    
    // Define a function to update user information
    function updateUserInfo(string memory _name, string memory _email) public {
        // TODO: Update user information in the mapping
        userMapping[msg.sender].name = _name;
        userMapping[msg.sender].email = _email;
    }
    
    // Define a function to delete user information
    function deleteUser() public {
        // TODO: Delete user information from the mapping
      delete userMapping[msg.sender];
    }
}
```
