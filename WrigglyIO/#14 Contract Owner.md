The problem is to return the address of the owner of the contract
```
Example 1:

  Input:
  Output: 0x123
  Explanation: This is because this is the address of the owner of the contract

Constraints:

  returnOwner() should only be allowed to be called by the contract creator.

Hints
  Create a constructor() to hold the address of the owner. [Hint: use msg.sender]
  Create a function returnOwner() which returns the address of the owner. This returnOwner() can only be called by the owner (that we set using constructor()). If some other address tries to call this returnOwner() it should revert with this statement -You are not the owner Note- - Function will be public.


```

### Solution 

```
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.4;

contract Owner {
    address public owner;

    constructor() {
      owner = msg.sender;
    }

    function returnOwner() public view returns (address) {
      return owner;
    }
}
```
