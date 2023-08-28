Structs allow you to create more complicated data types that have multiple properties.

Example
```
struct Person {
uint age;
string name;
}
```
Solution

```
pragma solidity >=0.5.0 <0.6.0;

contract ZombieFactory {

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    // start here ,Create a struct named Zombie. , Our Zombie struct will have 2 properties: name (a string), and dna (a uint).

    struct Zombie {
        string name;
        uint dna;
    }

}
```
