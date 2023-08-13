### Implement the ERC20's _mint(), _burn(), and getBalance() functions.

```
Example 1:

  Input: constructor(), _mint(100), _burn(50), getBalance()
  Output: [{},{},"50"]
  Explanation: The first call to the constructor will set the owner to the sender's address. The call to _mint() will mint the specified amount of tokens to the owner's address using the mapping. The call to _burn() will remove the specified amount of tokens from the owner's address. The call to getBalance() will return the balance of tokens in the sender's address.

Constraints:

  The function should return the balance of tokens in the sender's address.

Hints

  Create a mapping of addresses to token.
  For the constructor, set the owner to the sender's address.
  For the _mint function, add the specified amount to the sender's address using the mapping.
  For the _burn function, take out the specified amount from the sender's address using the mapping.
```

### Solution

```
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/utils/math/SafeMath.sol";

contract WrigglyToken is ERC20 {
    using SafeMath for uint256;

    // TODO: Create mapping to keep track of the balance of each address
    mapping (address => uint) public balanceMap;

    address public owner;

    constructor() ERC20("My Token", "MTKN") {
        // TODO
        owner = msg.sender;
    }

    function _mint(uint256 amount) public {
        // TODO
        balanceMap[owner] += amount;
        
    }

    function _burn(uint256 amount) public {
        // TODO
        balanceMap[owner] -= amount;
    }

    function getBalance() public view returns (uint256){
        // TODO
        return balanceMap[owner];
    }
}
```
