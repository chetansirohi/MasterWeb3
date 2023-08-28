### Write a Solidity smart contract that allows users to store and retrieve a string value. The contract should have two functions: set and get. The set function should take a string parameter and store it in the contract. The get function should return the stored string.

```
Example 1:

  Input: [get(), set(treasure), get()]
  Output: ["", {}, "treasure"]
  Explanation: If the contract has just been initialized it will start with nothing in its storedString. Only after setting something will we be able to get it.

Constraints:
  value will be of type string

Hints
  How would you implement a getter and setter in another language?

```
### Solution

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract StringStorage {
    string private storedString;

    function set(string memory value) public {
        // TODO
       storedString = value;
    }

    function get() public view returns (string memory) {
        // TODO
      return storedString;
    }
}
```
