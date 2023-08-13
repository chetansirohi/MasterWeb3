### We're given a function definition for sumIfEvenAndLessThan99 which goes through the nums array and adds a num to the variable total if it's even and less than 99. However, the way it's implemented is not gas efficient. Modify the sumIfEvenAndLessThan99 function and optimize the code.

```
Example 1:

  Input: nums = [1,2,3,4,5,100]
  Output: true
  Explanation: With optimized code, gasOptimized should return true.

Constraints:

  gasUsed needs to be optimized.

Hints
  Replacing memory with calldata
  Loading state variable to memory
  Replace for loop i++ with ++i
  Caching array elements
  Short circuit

```

### Solution
```
pragma solidity ^0.8.4;

contract Solution {
    uint public total;
    uint gasUsed;

    function sumIfEvenAndLessThan99(uint[] calldata nums) external {
        uint startGas = gasleft();
        uint _total = total;
        uint len = nums.length;

        for (uint i = 0; i < len; ) {
            uint num = nums[i];
            if (num % 2 == 0 && num < 99) {
                _total += num;
            }
            unchecked {
                ++i;
            }
        }

        total = _total;
    
        gasUsed = startGas - gasleft();
    }

    function gasOptimized(uint optimizedGas) public view returns (bool){
        if(gasUsed < optimizedGas){
            return true;
        }
        else{
            return false;
        }
    }
}
```
