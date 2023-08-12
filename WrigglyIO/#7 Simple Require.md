Another fundamental web3 problem when working with smart contracts is handling errors and exceptions that may occur during contract execution.

When a smart contract is executed, it may encounter errors or exceptions due to various reasons such as invalid input parameters, insufficient funds, or unexpected contract states. Handling these errors and exceptions is important to prevent unexpected behavior and ensure the integrity of the contract and its data.

In Solidity, errors and exceptions can be handled using various mechanisms such as the require, assert, and revert statements. These statements allow developers to check for certain conditions and revert the transaction if the condition is not met or throw an exception if the condition is not possible.

When interacting with smart contracts through Web3.js, it's important to handle these errors and exceptions properly to prevent loss of funds or other unexpected behavior. Web3.js provides methods such as send and call that can be used to execute contract functions and handle errors and exceptions that may occur during execution.

```
Example 1:

  Input: a = 3, b = 2
  Output: 1
  Explanation: 3 - 2 = 1

Example 2:

  Input: a = 2, b = 3
  Output: revert error: Overflow error
  Explanation: Because 3-2 would result in a not being a uint256, we must require that it does not fall outside its constraints

Constraints:

  0 <= a <= 2^256-1
  0 <= b <= 2^256-1

Hints
  `require` statements throw reverts when the logic in it resolves to false

```

### Solution

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleRequire {
    function subtract(uint256 a, uint256 b) public pure returns (uint256) {
        // Check for overflow
        require(a > b, "Overflow error");
        return a - b;
    }
}
```
