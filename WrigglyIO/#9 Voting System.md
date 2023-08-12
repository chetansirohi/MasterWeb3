Create a Solidity contract called Voting that allows users to vote on a given set of proposals. The vote(uint256 proposal) allows users to vote for a given proposal. Each user can only vote once and can only vote for a valid proposal, so make sure to include require statement in your code to check for these. The getProposal(uint256 proposal) returns the name of the proposal with the given index. The getVotes(uint256 proposal) returns the number of votes received by the proposal with the given index. Make sure to use require to check if the index in getProposal and getVotes is valid.
```
Example 1:

  Input: 1
  Output: 1
  Explanation: There are 2 proposals. proposals[0] has 0 votes and proposals[1] has 1 vote. getVotes(1) should return 1 since that proposal has 1 vote.

Constraints:

  The function should return the number of votes received by the proposal.

Hints
  A function vote(uint256 proposal) that allows users to vote for a given proposal. Each user can only vote once and can only vote for a valid proposal.
  A function getProposal(uint256 proposal) that returns the name of the proposal with the given index.
  A function getVotes(uint256 proposal) that returns the number of votes received by the proposal with the given index.

```

### Solution

```
pragma solidity ^0.8.4;

contract Voting {

    string[] public proposals;
    mapping(uint256 => uint256) public votes;
    mapping(address => bool) public voted;

    constructor() {
        proposals = ["Proposal 1", "Proposal 2"];
    }

    function vote(uint256 proposal) public {
        // TODO: Implement vote function, check if user has already voted, check if a proposal in proposals is valid
        require(!voted[msg.sender], "Already voted");
        require(proposal < proposals.length, "Invalid proposal");
        voted[msg.sender] = true;
        votes[proposal]++;
    }

    function getProposal(uint256 proposal) public view returns (string memory) {
        // TODO: Implement getProposal function
        require(proposal < proposals.length, "Invalid proposal");
        return proposals[proposal];
    }

    function getVotes(uint256 proposal) public view returns (uint256) {
        // TODO: Implement getVotes function
        require(proposal < proposals.length, "Invalid proposal");
        return votes[proposal];
    }
    
}
```
