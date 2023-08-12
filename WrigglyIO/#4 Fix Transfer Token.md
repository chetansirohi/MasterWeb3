### Looks like this transfer function is wrong. A user is not able to transfer 10 coins even though they have 20 coins. Can you fix it?
```
Example 1:

  Input: to = "0x123", amount = 10
  Output: false
  Explanation: The user with address msg.sender (i.e., the person calling the transfer function) has a balance of 0, so the transfer should fail.

Example 2:

  Input: to = "0x123", amount = 20
  Output: true
  Explanation: The user has a balance of 20, and is attempting to transfer 20 tokens to the address 0x123. The transfer should succeed.
  
Constraints:

  The total supply of the token should be a positive integer value.
  The balance of each account should be a non-negative integer value.
  The transfer amount should be a non-negative integer value.

Hints
  Should the user's balance exceed the transfer amount?
  Check lines 29-33

```

### Solution

```
pragma solidity ^0.8.4;

contract ERC20 {
    mapping(address => uint256) private _balances;

    /**
     * @dev Moves `amount` of tokens from `from` to `to`.
     *
     * This internal function is equivalent to {transfer}, and can be used to
     * e.g. implement automatic token fees, slashing mechanisms, etc.
     *
     * Emits a {Transfer} event.
     *
     * Requirements:
     *
     * - `from` cannot be the zero address.
     * - `to` cannot be the zero address.
     * - `from` must have a balance of at least `amount`.
     */
    function _transfer(
        address from,
        address to,
        uint256 amount
    ) internal virtual {
        require(from != address(0), "ERC20: transfer from the zero address");
        require(to != address(0), "ERC20: transfer to the zero address");

        uint256 fromBalance = _balances[from];
        require(
            fromBalance >= amount,
            "ERC20: transfer amount exceeds balance"
        );
        _balances[from] = amount - fromBalance;
        // Overflow not possible: the sum of all balances is capped by totalSupply, and the sum is preserved by
        // decrementing then incrementing.
        _balances[to] += amount;
    }

    function transfer(address to, uint256 amount)
        public
        virtual
        returns (bool)
    {
        address owner = msg.sender;
        _transfer(owner, to, amount);
        return true;
    }
}
```
