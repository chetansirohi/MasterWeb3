### The problem is to create a Solidity smart contract to manage a simple lottery. The contract should allow users to buy a ticket with a unique ID, and the contract should be able to draw a winner randomly from all the purchased tickets.

```
Example 1:

  Input: ["0x123", "0"]
  Output: ["0x123", "0", "0", ....]
  Explanation: getTeamPlayers() would only contain jersey number 0 with the address 0x123

Constraints:

  The function should emit an event when ether is transferred.

Hints
  Create an array(address type) which stores only 16 elements.
  getTeamPlayers() - To return the entire array elements.
  selectJerseyNumber() - It will take only one argument of uint type and returns the players address from the array created above. a) The argument passed into the function must be greater than equal to zero and less than equal to 15. [Hint - Use require]
  addPlayer: Allows a new player to be added to the team by specifying their Ethereum address and the desired jersey number (which must be between 0 and 15 and must not already be assigned to another player).
  removePlayer: Allows a player to be removed from the team by specifying their jersey number (which must be between 0 and 15 and must already be assigned to a player).
  updatePlayerAddress: Allows the Ethereum address of a player to be updated by specifying their jersey number (which must be between 0 and 15 and must already be assigned to a player) and their new address.

```

### Solution 

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

contract Team {

    int[16] public teamPlayers;

    function initializeTeam() public {
        for (uint i = 0; i < teamPlayers.length; i++) {
            teamPlayers[i] = -1;
        }
    }

    function getTeamPlayers() public view returns (int[16] memory) {
      return teamPlayers;
    }

    function selectJerseyNumber(uint jerseyNumber) public view returns (int) {
      require(jerseyNumber>=0,"Invalid jerseyNumber");
      require(jerseyNumber<=15,"Invalid jerseyNumber");
      return teamPlayers[jerseyNumber];
    }

    function addPlayer(int playerAddress, uint jerseyNumber) public {
      require(jerseyNumber>=0,"Invalid jerseyNumber");
      require(jerseyNumber<=15,"Invalid jerseyNumber");
      require(teamPlayers[jerseyNumber] == -1, "Jersey number already assigned");
      teamPlayers[jerseyNumber] = playerAddress;
    }

    function removePlayer(uint jerseyNumber) public {
      require(jerseyNumber>=0,"Invalid jerseyNumber");
      require(jerseyNumber<=15,"Invalid jerseyNumber");
      delete teamPlayers[jerseyNumber];
    }

    function updatePlayerAddress(int newAddress, uint jerseyNumber) public {
      require(jerseyNumber>=0,"Invalid jerseyNumber");
      require(jerseyNumber<=15,"Invalid jerseyNumber");
      require(teamPlayers[jerseyNumber] != -1, "Jersey number not assigned");
      teamPlayers[jerseyNumber] = newAddress;
    }
}
```
