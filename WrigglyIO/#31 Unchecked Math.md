### Overflow and underflow of numbers in Solidity 0.8 throw an error. This can be disabled using a keyword. It is typically used in cases where the developer knows that the arithmetic operation will not result in overflow or underflow, and wants to optimize the gas cost of the operation by avoiding the checks. Your task is to modify the code to avoid overflow/underflow by using a keyword.

```
Example 1:

  Input: x = 2**256 - 1, y = 1
  Output: 0
  Explanation: (2**256 - 1) + 1 = 0

Constraints:

  You should prevent overflow or underflow

Hints
  
  Use the unchecked keyword

```

### Solution

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract UncheckedMath {
    function add(uint y) external pure returns (uint) {
      unchecked{
          return (2**256 - 1) + y;
      }
        
    }

    function sub(uint x, uint y) external pure returns (uint) {
        unchecked{return x - y;}
    }
}
```
