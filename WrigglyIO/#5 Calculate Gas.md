### Edit the boilerplate function to calculate how much gas it cost to increment state variable "c".
```
Example 1:

  Input:
  Output: 5958
  Explanation: This is because this much gas was used for incrementing a state variable by 1

Hints
  What solidity functions provide you information about gas

```

### Solution

```
pragma solidity ^0.8.4;

contract Gas {
    uint public c = 1;

    function calculateGas() external returns(uint _gasUsed) {
      //Todo
      uint gasUsed = gasleft();
        ++c;
      return gasUsed - gasleft();
    }
}
```
