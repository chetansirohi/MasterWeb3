### Using the imported ERC20 contract build your own token with initialSupply and mint all of them to yourself.

```
Example 1:

  Input: constructor("100"), getBalance()
  Output: ["100"]
  Explanation: The first call to the constructor will mint the initial number of tokens. The call to getBalance() will return the balance of tokens in the sender's address.
  Constraints:
  
  The function should return the balance of tokens in the sender's address.

Hints

  Use ERC20's built in _mint() function.
  Set the owner to the address of the account that's sending the transaction.
  Use ERC20's balanceOf() function.

```

### Solution

```
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/utils/math/SafeMath.sol";

contract WrigglyToken is ERC20 {
    using SafeMath for uint256;

    address public owner;

    constructor(uint256 initialSupply) ERC20("My Token", "MTKN") {
        // TODO
      owner = msg.sender;
      _mint(owner, initialSupply );
    }

    function getBalance() public view returns (uint256) {
        // TODO
      return balanceOf(owner);
    }
}
```
