You are tasked with creating a smart contract that allows users to mint non-fungible tokens (NFTs) with metadata stored on IPFS and keep track of the ownership of these tokens. The NFTs must conform to the ERC721 standard, which is a widely used standard for NFTs on the Ethereum blockchain. The mint function should mint a new token with its metadata stored on IPFS and assign it to an address. The ownerOf function should return the address that owns a specific token. In addition, you should implement a function that returns the IPFS hash of a specific token's metadata, given its token ID. This function should be useful for applications that need to access the metadata of a token.

```
Example 1:

  Input: mint("0xd81249D2a8e19614b8629d39f46fAca9Df1357f4", "2", "My_NFT_IPFS"), tokenIPFSHash("2")
  Output: [{}, "My_NFT_IPFS"]
  Explanation: In the first call to mint we will create the token under that user for that ID and ipfsHash. In the second call we will retrieve the IPFS's hash for a token's metadeta using the tokenId.

Constraints:

  The function should return the owner of a minted NFT.

Hints
  In the mint function use _mint method inherited from ERC721 to mint a new token.
  Call your method _setTokenIPFSHash to store the IPFS hash of the token's metadata.

```

### Solution

```
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/utils/math/SafeMath.sol";

contract MyNFT is ERC721 {
    using SafeMath for uint256;

    mapping(uint256 => address) private _tokenOwner;
    mapping(uint256 => string) private _tokenIPFSHash;

    constructor(
        string memory name,
        string memory symbol
    ) ERC721(name, symbol) {}

    function mint(address to, uint256 tokenId, string memory ipfsHash) public {
        // TODO
      _mint(to, tokenId);
      _setTokenIPFSHash(tokenId, ipfsHash);
    }

    function ownerOf(
        uint256 tokenId
    ) public view virtual override returns (address) {
        // TODO
      return _tokenOwner[tokenId];
    }

    function tokenIPFSHash(
        uint256 tokenId
    ) public view returns (string memory) {
        // TODO
      return _tokenIPFSHash[tokenId];
    }

    function _setTokenIPFSHash(
        uint256 tokenId,
        string memory ipfsHash
    ) internal {
        // TODO
      _tokenIPFSHash[tokenId] = ipfsHash;
    }
}
```
