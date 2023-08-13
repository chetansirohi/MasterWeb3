### You are building a smart contract that allows users to store and retrieve data on a decentralized network. You want to make it easy for users to store data by allowing them to simply send ether to the contract address along with their data. You also want to make it easy for users to retrieve their data by allowing them to call a getData function on the contract.

```
Example 1:

  Input: Hello World
  Output: Hello World
  Explanation: Passing in "Hello World" and an ethereum value of 0.1 will store the data

Constraints:

  Map the senders address to the data they are storing in `storeData`

Hints

  Pass the data through `storeData`
  Require that the user sends ether to the contract to store the data

```

### Solution

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract DataStorage {
    mapping(address => string[]) public userData;

    function storeData(string memory data) public payable {
        // TODO
        require(msg.value > 0, "Data storage fee must be greater than 0");
        userData[msg.sender].push(data) ;
    }

    function getData(uint256 index) public view returns (string memory) {
        // TODO
        require(index < userData[msg.sender].length, "Index out of bounds");
        return userData[msg.sender][index];
    }

    function getDataCount() public view returns (uint256) {
        // TODO
        return userData[msg.sender].length;
    }
}
```
