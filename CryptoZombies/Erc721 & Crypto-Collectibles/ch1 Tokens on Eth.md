ERC721 tokens are not interchangeable since each one is assumed to be unique, and are not divisible. You can only trade them in whole units, and each one has a unique ID. So these are a perfect fit for making our zombies tradeable.

Solution

Declare our pragma version at the top of the file (check previous lessons' files for the syntax).

This file should import from zombieattack.sol.

Declare a new contract, ZombieOwnership, that inherits from ZombieAttack. Leave the body of the contract empty for now.

```

pragma solidity >=0.5.0 <0.6.0;

import "./zombieattack.sol";

contract ZombieOwnership is ZombieAttack{

}
```
