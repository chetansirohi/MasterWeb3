### The generateKeyPair function should return a randomly generated public and private key

```
Example 1:

  Input: generateKeyPair
  Output: [{"0":"0x2fa2ccac4ae606fc070641354b4fb5ddb36fc7748113e7b2a42f3809b380d2d9","1":"0xdd651562aabd2c8576db9f5f45a4ce780d43803cc21409380f880e50493490c5"}]
  Explanation: Randomly generated (public, private) key

Constraints:

  The generateKeyPair() function should return a randomly generated (public, private) key.

Hints
  For generatePrivateKey() use keeccak256 along with the block's timestamp and eithers the block's difficulty or prevrandao.
  For computePublicKey() use keeccak256 along with the _privateKey.

```

### Solution

```
pragma solidity ^0.8.0;

contract KeyPair {
    // Declare a private key variable here
    bytes32 private privateKey;
    bytes32 private publicKey;

    // Declare a function to generate a new key pair
    function generateKeyPair() public returns (bytes32, bytes32) {
        // TODO: Call a function to generate a new private key
        privateKey = generatePrivateKey();
        publicKey = computePublicKey(privateKey);

        // TODO: Compute the corresponding public key

        return (publicKey, privateKey);
    }

    // Implement a function to generate a new private key
    function generatePrivateKey() private returns (bytes32) {
        // TODO: You can use Solidity's built-in cryptographic functions to generate a random private key
        return keccak256(abi.encodePacked(block.timestamp, block.difficulty));
    }

    // Implement a function to compute the corresponding public key
    function computePublicKey(bytes32 _privateKey) private pure returns (bytes32) {
        // TODO: You can use Solidity's built-in cryptographic functions to compute the public key from the private key
        return keccak256(abi.encodePacked(_privateKey));
    }
}
```
