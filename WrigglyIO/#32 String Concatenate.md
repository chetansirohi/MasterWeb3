### Concatenation of string in solidity can't be done simply by doing str1 + str2. We must use a special function to achieve this.

```
Example 1:

  Input: str1 = "Hello ", str2 = "World!"
  Output: Hello World!
  Explanation: 'Hello ' + 'World!' = 'Hello World!'

Constraints:

  Concatenate the two strings.

Hints

  Use the bytes function to convert the string into bytes.

```

### Solution

```
pragma solidity ^0.8.0;

contract Concatenate {
    function concat(string memory str1, string memory str2) public pure returns (string memory) {
        // TODO
        return string(abi.encodePacked(str1,str2));
    }
}
```
