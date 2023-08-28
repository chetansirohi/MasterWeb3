### The problem is to create a Solidity smart contract to manage a simple lottery. The contract should allow users to buy a ticket with a unique ID, and the contract should be able to draw a winner randomly from all the purchased tickets. The tickets variables holds all the tickets. The ticketCount represents how amny tickets have been purchased. The winner is the address of the winner of the lottery.

```
Example 1:

  Input: 2
  Output: 0x123
  Explanation: Assuming at least 1 ticket has been purchased, the getWinner() function should return the address of the lottery winner.

Constraints:

  You can assume tickets will never have more than 100 slots

Hints
  buyTicket: This function should create a new ticket with the given ID and add it to the tickets array. The function should also increment the ticketCount variable.
  drawWinner: This function should select a random ticket from the tickets array and declare the owner of the selected ticket as the winner. The function should also transfer the entire balance of the contract to the winner's address and reset the ticketCount variable.
  getWinner: Require that someone has won the lottery and return the winner.

```

### Solution

```
pragma solidity ^0.8.4;

contract Lottery {

    struct Ticket {
        uint id;
        address owner;
    }
    
    Ticket[100] public tickets;
    uint public ticketCount;
    address payable winner;

    constructor(uint _ticketCount) {
        // TODO: Initialize ticketCount
        ticketCount = _ticketCount;
    }
    
    function buyTicket(uint id) public payable {
        // TODO: Implement the buyTicket function. This function should create a new ticket with the given ID and add it to the tickets array. 
        // The function should also increment the ticketCount variable and transfer the ticket price (1 ether) from the buyer to the contract.
        require(msg.value >= 1 ether, "Ticket price is 1 ether.");     
        require(ticketCount < 100, "All tickets sold");
        tickets[ticketCount] = Ticket(id, msg.sender);
        ticketCount++;
        
    }
    
    function drawWinner() public {
        // TODO: Implement the drawWinner function. We have already defined a randomly generated winnerIndex.
        //       This owner of this ticket will be set as the winner of the lottery.
        // The function should also transfer the entire balance of the contract to the winner's address and reset the ticketCount variable to 0.
        require(ticketCount > 0, "No tickets sold.");
        uint winnerIndex = uint(keccak256(abi.encodePacked(block.timestamp, block.prevrandao, tickets.length))) % tickets.length;
        winner = payable(tickets[winnerIndex].owner);
        winner.transfer(address(this).balance);
        ticketCount = 0;
    }

    function getWinner() public view returns (address) {
        // TODO: Require there has been a winner and return the winner
        require(winner != address(0), "Please implement drawWinner");
        return winner;
    }
}
```
