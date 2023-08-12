### Write a function that adds a new item to an inventory. Your task is to add a modifier that only allows the owner of the contract to add items to the inventory. You can assume that the owner's address is stored in a state variable called 'owner'.
```
Example 1:

  Input: _name = "shoes", _price = 100
  Output: [{"_name":"shoes","_price":100}]
  
Example 2:

  Input: _name = "book", _price = 10"
  Output: [{"_name":"book","_price":10}]
  
Constraints:

  Only the owner of the contract should be able to add items.

Hints

  Use a struct to define the properties of an item.
  Use a modifier to restrict access to the function.

```

### Solution

```
pragma solidity ^0.8.4;

contract Solution {
    struct Item {
        string name;
        uint256 price;
    }

    Item[] public inventory;
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    function addItemToInventory(
        string memory _name,
        uint256 _price
    ) public onlyOwner {
        // TODO
      inventory.push(Item(_name,_price));
    }

    modifier onlyOwner() {
        _;
    }

    function getInventory() public view returns (Item[] memory) {
        // TODO
      return inventory;
    }

    function clearInventory() private onlyOwner {
        // TODO
      delete inventory;
    }
}

```
