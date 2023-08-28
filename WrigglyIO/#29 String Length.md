### In this contract, the getLength function takes a string parameter and returns an unsigned integer (uint) representing the length of the string. Note that you can't simply return str.length.

```
Example 1:

  Input: str = 'Hello World'
  Output: 11
  Explanation: The length of the string 'Hello World' is 11

Constraints:

  Return the length of the string str

Hints

  Use the bytes function to convert the string into bytes.

```

### Solution

```
pragma solidity ^0.8.0;

contract StringLength {
    function getLength(string memory str) public pure returns (uint) {
        // TODO
        return bytes(str).length;
    }
}
```
