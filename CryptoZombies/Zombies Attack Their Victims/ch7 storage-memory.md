Storage refers to variables stored permanently on the blockchain. Memory variables are temporary, and are erased between external function calls to your contract

State variables (variables declared outside of functions) are by default storage and written permanently to the blockchain, while variables declared inside functions are memory and will disappear when the function call ends

Solution

When a zombie feeds on some other lifeform, its DNA will combine with the other lifeform's DNA to create a new zombie.

1.Create a function called feedAndMultiply. It will take two parameters: _zombieId (a uint) and _targetDna (also a uint). This function should be public.

2.We don't want to let someone else feed our zombie! So first, let's make sure we own this zombie. Add a require statement to verify that msg.sender is equal to this zombie's owner (similar to how we did in the createRandomZombie function).

3.We're going to need to get this zombie's DNA. So the next thing our function should do is declare a local Zombie named myZombie (which will be a storage pointer). Set this variable to be equal to index _zombieId in our zombies array.


```
pragma solidity >=0.5.0 <0.6.0;

import "./zombiefactory.sol";

contract ZombieFeeding is ZombieFactory {

  // Start here
  function feedAndMultiply(uint _zombieId, uint _targetDna) public {
      // checks zombies owned by msg.sender, zombiesToOwner created in zombiefactoy.sol

      require( msg.sender == zombieToOwner[_zombieId] );

      //as is required to store onto blockchain

      Zombie storage myZombie = zombies[_zombieId];
  }

}
```
