### Create a Solidity smart contract that can check whether it has expired or not based on a specific duration of time. Set the creationTime to the current block timestamp. In the onTime() function set the expirationTime to 1 day after the creationTime. In the expire function set the expirationTime 1 day before the creationTime.

```
Example 1:

  Input: creationTime: 4/10/2023 6:06 pm. Then we call onTime().
  Output: false
  Explanation: This is because when we run out test case, it hasn't been 1 day since the contract has been deployed, so it hasn't expired.

Constraints:

  Check if the current block timestamp is greater than or equal to the expiration time

Hints
  Use block.timestamp
  Set expiration time to 1 day after creationTime.
  Use days modifier

```

### Solution

```
pragma solidity ^0.8.0;

contract MyContract {
    uint public creationTime;
    uint public expirationTime;

    constructor() {
        // TODO: Set creationTime to block timestamp
        creationTime = block.timestamp;
    }

    function onTime() public {
        // TODO: Set expirationTime to be after creationTime
        expirationTime = creationTime + 1 days;
    }

    function expire() public {
        // TODO: Set expirationTime to be before creationTime
        expirationTime = creationTime - 1 days;
    }

    function isExpired() public view returns (bool) {
        return block.timestamp >= expirationTime;
    }
}
```
