### Write a problem that compares strings. NOTE: Solidity doesn't have direct comparison so you will need to convert the strings to something solidity does understand in order to get the correct answer.

```
Example 1:

  Input: a = "Hello", b = "Hello"
  Output:
  Explanation: The two strings are equal.

Constraints:

  Solidity does not have direct string comparison built in.

Hints
  
  Make sure to use the built-in method `keccack256`
  How can we convert the string to something that `keccack256` will understand?

```

### Solution
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract StringComparator {
    function compareStrings(
        string memory a,
        string memory b
    ) public pure returns (bool) {
        // TODO
        return keccak256(abi.encodePacked(a)) == keccak256(abi.encodePacked(b));
    }
}
```
