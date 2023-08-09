So in this case we could declare it as a view function, meaning it's only viewing the data but not modifying it

```
function sayHello() public view returns (string memory) {
```

Solidity also contains pure functions, which means you're not even accessing any data in the app

```
function _multiply(uint a, uint b) private pure returns (uint) {
  return a * b;
}
```

Solution 

1. Create a private function called _generateRandomDna. It will take one parameter named _str (a string), and return a uint. Don't forget to set the data location of the _str parameter to memory.

2. This function will view some of our contract's variables but not modify them, so mark it as view.

3. The function body should be empty at this point — we'll fill it in later.

```
pragma solidity >=0.5.0 <0.6.0;

contract ZombieFactory {

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    struct Zombie {
        string name;
        uint dna;
    }

    Zombie[] public zombies;

    function _createZombie(string memory _name, uint _dna) private {
        zombies.push(Zombie(_name, _dna));
    }

    // start here
    function _generateRandomDna(string memory _str) private view returns( uint ){

    }

}
```
   
