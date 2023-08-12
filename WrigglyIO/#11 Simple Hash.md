The keccak256 function is a cryptographic hash function that is used to convert input data of any size into a fixed-size output (256 bits in this case) in a way that is computationally infeasible to reverse. It was developed by Guido Bertoni, Joan Daemen, Michaël Peeters, and Gilles Van Assche, and was selected as the winner of the NIST hash function competition in 2012.

The keccak256 function takes an input string or byte array and returns a 256-bit hash value that is unique to the input data. The output of keccak256 is generally represented as a hexadecimal string, which is a sequence of 64 characters that represent the 256 bits of the hash value.

In the context of blockchain and smart contract development, keccak256 is commonly used to implement various cryptographic functions such as:

Creating a unique identifier for a specific input data
Securing sensitive information such as passwords or private keys
Creating a digital signature to ensure the authenticity and integrity of data
Implementing a proof-of-work algorithm to secure the network
In this question, implement a simple hash function hash that returns a 256-bit hash of an input string and return the value by getting the value with the function getHashValue.

```
Example 1:

  Input: _message = "Hello world"
  Output: [{},"0xdb99debe7fc546756227481ecaf5136f5b86180d99c5666a14421367c7187e5c"]
  
Constraints:

  return from the public view of the contract instance
  use `keccak256` to hash the input string

Hints
  You will need to convert the input string to bytes before getting its hash.
```

### Solution

```
pragma solidity ^0.8.0;

contract SimpleHash {
    bytes32 public hashValue;

    function hash(string memory _message) public {
        // TODO
      hashValue = keccak256(abi.encodePacked(_message));
    }

    function getHashValue() public view returns (bytes32) {
        // TODO
      return hashValue;
    }
}
```
