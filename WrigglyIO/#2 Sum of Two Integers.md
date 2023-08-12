### Calculate the sum of two integers a and b.

```
Example 1:

  Input: a = 1, b = 2
  Output: 3
  Explanation: 1 + 2 = 3
  Example 2:

  Input: a = 2, b = -2
  Output: 0
  Explanation: 2 + (-2) = 0
  
Constraints:

  0 <= a <= 10^5
  0 <= b <= 10^5

Hints
  Add the two numbers in O(1) time.
```

Solution
```
  pragma solidity >=0.4.22 <0.9.0;

contract Solution {
    /**
     * @param {uint256} a
     * @param {uint256} b
     * @return uint256
     */
    function sumOfTwoIntegers(uint256 a, uint256 b)
        public
        pure
        returns (uint256)
    {
        return a + b;
    }
}
```
