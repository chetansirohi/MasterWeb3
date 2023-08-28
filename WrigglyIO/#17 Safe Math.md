In this contract use the @openzeppelin/contracts library, SafeMath to ensure that you protect your contract against potential vulernabilites like integer overflow and underflow conditions.

You see reference the @openzeppelin/contracts SafeMath Implementation here.

It's important to note that since Solidity version 0.8.0, the compiler now includes overflow and underflow protection for basic arithmetic operations with built-in integer types by default. However, if you need to perform more complex arithmetic operations or use custom data types, it's still a good practice to use the SafeMath library to prevent potential vulnerabilities.

```
Constraints:

  Only the owner of the contract should be able to add items.

Hints

  Reference the `@openzeppelin/contract` docs to learn more about the SafeMat.sol file you are using.
```

### Solution

```
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/utils/math/SafeMath.sol";

contract SafeMathExample {
    using SafeMath for uint256;

    uint256 public value;

    function add(uint256 x, uint256 y) public {
        // TODO
      value= x.add(y);
    }

    function sub(uint256 x, uint256 y) public {
        // TODO
      value=x.sub(y);
    }

    function mul(uint256 x, uint256 y) public {
        // TODO
      value=x.mul(y);
    }

    function div(uint256 x, uint256 y) public {
        // TODO
      value=x.div(y);
    }

    function get() public view returns (uint256) {
        // TODO
      return value;
    }
}

```
