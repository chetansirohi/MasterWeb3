Create a smart contract in the Solidity programming language that allows users to mint non-fungible tokens (NFTs) and keep track of the ownership of these tokens. The contract should be based on the ERC721 standard, which is a widely used standard for NFTs on the Ethereum blockchain.

This contract inherits from the OpenZeppelin implementation of ERC721 and adds a mapping to store the owner of each token. The mint function is used to mint a new token and assign it to an address. The ownerOf function returns the address that owns a specific token.
```
Example 1:
  
  Input: mint("0xd81249D2a8e19614b8629d39f46fAca9Df1357f4", "2"), ownerOf("2")
  Output: [{}, "0xd81249D2a8e19614b8629d39f46fAca9Df1357f4"]
  Explanation: In the first call to mint we will create the token under that user for that ID and in the second call we will retrieve the owner

Constraints:

  The function should return the owner of a minted NFT.

Hints
  
  Maintain a mapping between the user addresses and the tokens minted.
  Use the built in `safeMint` method.
```

### Solution

```
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/utils/math/SafeMath.sol";

contract MyNFT is ERC721 {
    using SafeMath for uint256;

    mapping(uint256 => address) private _tokenOwner;

    constructor(
        string memory name,
        string memory symbol
    ) ERC721(name, symbol) {}

    function mint(address to, uint256 tokenId) public {
        // TODO , mint the NFT and ownership of minted NFT to the _to address
      require(to != address(0), "mint to zero address");
      _mint(to,tokenId);
      _tokenOwner[tokenId] = to;
          
    }

    function ownerOf(
        uint256 tokenId
    ) public view virtual override returns (address) {
        // TODO
      
      return _tokenOwner[tokenId];
    }
}
```
