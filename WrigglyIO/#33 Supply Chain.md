### The problem is to create a smart contract in Solidity that manages a simple supply chain. The contract should allow users to register new products with a name and a unique ID, transfer products from one user to another, and retrieve the current owner of a product.

```
Example 1:

  Input: 0
  Output: 0x123
  Explanation: Assuming at least 1 product has been registered, the getProductOwner(0) should return the address of the 1st product.

Constraints:

  The function should emit an event when ether is transferred.

Hints

  A function called registerProduct that takes a string parameter name and creates a new product with a unique ID and initializes the owner to the user who registered the product.
  A function called transferProduct that takes a uint parameter id and an address parameter newOwner and transfers ownership of the product with the corresponding ID to the new owner. The function should revert the transaction if the caller is not the current owner of the product.
  A function called getProductOwner that takes a uint parameter id and returns the address of the current owner of the product with the corresponding ID in the products mapping.
```

### Solution

```
pragma solidity ^0.8.4;

contract SupplyChain {
    
    address public owner;
    
    struct Product {
        string name;
        address owner;
    }
    
    mapping(uint => Product) public products;
    uint public productCount;
    
    constructor() {
        // TODO: set the contract creator as the owner
      owner = msg.sender;
    }
    
    function registerProduct(string memory name) public {
        // TODO: create a new Product with a unique ID and initialize the owner to the caller
        productCount++;
        products[productCount]= Product(name, owner);
    }
    
    function transferProduct(uint id, address newOwner) public {
        // TODO: transfer ownership of the product with the corresponding ID to the new owner
        // The function should revert the transaction if the caller is not the current owner of the product.
        require(products[id].owner == msg.sender,"Not Owner");
        products[id].owner= newOwner;
        
    }
    
    function getProductOwner(uint id) public view returns (address) {
        // TODO: return the address of the current owner of the product with the corresponding ID in the `products` mapping
        return products[id].owner;
    }
    
}
```
