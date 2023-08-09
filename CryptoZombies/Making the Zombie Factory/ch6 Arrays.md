When you want a collection of something, you can use an array.

Example 
```
// Array with a fixed length of 2 elements:
uint[2] fixedArray;
// another fixed Array, can contain 5 strings:
string[5] stringArray;
// a dynamic Array - has no fixed size, can keep growing:
uint[] dynamicArray;
```

You can also create an array of structs. Using the previous chapter's Person struct:

```
Person[] people; // dynamic Array, we can keep adding to it
```
You can declare an array as public, and Solidity will automatically create a getter method for it.

Solution 

Create a public array of Zombie structs, and name it zombies.

```
pragma solidity >=0.5.0 <0.6.0;

contract ZombieFactory {

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    struct Zombie {
        string name;
        uint dna;
    }

    // start here
    Zombie[] public zombies;

}
```
