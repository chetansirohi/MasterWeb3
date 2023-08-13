### Write a hashing algorithm that will take in a value and hash it with the built-in solidity hashing function ripemd160. Learn about usecases for the ripemd160 hashing algorithm on GeeksForGeeks.

```

Example 1:

  Input: _message = "Hello, world"
  Output: ["0xdb99debe7fc546756227481ecaf5136f5b86180d99c5666a14421367c7187e5c"]

Constraints:

  return from the public view of the contract instance
  use `ripemd160` to hash the input string

Hints

  You will need to convert the input string to bytes before getting its hash.
```

### Solution

```
pragma solidity ^0.8.0;

contract Solution {
    function ripemdHash(string memory _message) public pure returns (bytes20) {
        // TODO
      return ripemd160(abi.encodePacked(_message));
    }
}
```
