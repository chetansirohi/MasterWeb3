```
function transferFrom(address _from, address _to, uint256 _tokenId) external payable;
```
The first way is the token's owner calls transferFrom with his address as the _from parameter, the address he wants to transfer to as the _to parameter, and the _tokenId of the token he wants to transfer.

```
function approve(address _approved, uint256 _tokenId) external payable;

function transferFrom(address _from, address _to, uint256 _tokenId) external payable;
```
The second way is the token's owner first calls approve with the address he wants to transfer to, and the _tokenID . The contract then stores who is approved to take a token, usually in a mapping (uint256 => address). Then, when the owner or the approved address calls transferFrom, the contract checks if that msg.sender is the owner or is approved by the owner to take the token, and if so it transfers the token to him.

Solution

1.Define a function named _transfer. It will take 3 arguments, address _from, address _to, and uint256 _tokenId. It should be a private function.

2.We have 2 mappings that will change when ownership changes: ownerZombieCount (which keeps track of how many zombies an owner has) and zombieToOwner (which keeps track of who owns what).

The first thing our function should do is increment ownerZombieCount for the person receiving the zombie (address _to). Use ++ to increment.

3.Next, we'll need to decrease the ownerZombieCount for the person sending the zombie (address _from). Use -- to decrement.

4.Lastly, we'll want to change zombieToOwner mapping for this _tokenId so it now points to _to.

5.I lied, that wasn't the last step. There's one more thing we should do.

The ERC721 spec includes a Transfer event. The last line of this function should fire Transfer with the correct information — check erc721.sol to see what arguments it's expecting to be called with and implement it here.


```
pragma solidity >=0.5.0 <0.6.0;

import "./zombieattack.sol";
import "./erc721.sol";

contract ZombieOwnership is ZombieAttack, ERC721 {

  function balanceOf(address _owner) external view returns (uint256) {
    return ownerZombieCount[_owner];
  }

  function ownerOf(uint256 _tokenId) external view returns (address) {
    return zombieToOwner[_tokenId];
  }

  // Define _transfer() here
  function _transfer(address _from, address _to, uint256 _tokenId) private{
      ownerZombieCount[_to]++;
      ownerZombieCount[_from]--;
      zombieToOwner[_tokenId]= _to;
      emit Transfer(_from, _to, _tokenId);
  }

  function transferFrom(address _from, address _to, uint256 _tokenId) external payable {

  }

  function approve(address _approved, uint256 _tokenId) external payable {

  }
}
```
