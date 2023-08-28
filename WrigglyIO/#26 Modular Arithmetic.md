In Solidity, addmod and mulmod are mathematical functions that perform addition and multiplication with modulo arithmetic respectively.

The reason to use addmod and mulmod instead of regular addition and multiplication is to prevent integer overflow or underflow errors that can occur when dealing with large numbers. If an integer overflows or underflows in Solidity, it will wrap around to a smaller number, which can cause unexpected behavior and potentially compromise the security of the contract.

### Write a method callAddMod and a method callMulMod that ensures that your contract is safe regardless of the paramters passed into it.

```
Example 1:

  Input: a = 4, b = 5, c = 3
  Output: callAddMod -- 0, callMulMod -- 2
  Explanation: We will add the two values and take the modulo in callAddMod and multiply the two and take the modulo for callMulMod

Constraints:

  This solution is required to prevent from overflow with very large numbers.

Hints

  Make sure to use the built-in methods `addmod` and `mulmod`
```

### Solution

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Test {
    function callAddMod(
        uint256 a,
        uint256 b,
        uint256 c
    ) public pure returns (uint) {
        // TODO
        
        return addmod(a,b,c);
    }

    function callMulMod(
        uint256 a,
        uint256 b,
        uint256 c
    ) public pure returns (uint) {
        // TODO\
        return mulmod(a,b,c);
        
    }
}
```
