### A pool can be in one of three states: Initialized, Finalized, Deactivated. Write a function to determine if the pool is in a valid state: Initialized

```
Example 1:

  Input: Initialized
  Output: [true]
  Explanation: Initialized matches the current pool state

Example 2:

  Input: lorem
  Output: [false]
  Explanation: lorem is not a valid pool state

Hints
  Make an enum State with three possible states
  Initialize the poolState to be a valid state in the constructor

```

#Solution

```
pragma solidity ^0.8.4;

contract Pool {
    //TODO: Create enum State
    enum State{
      Initialized, 
      Finalized, 
      Deactivated
    }
    State public poolState;

    constructor() {
        //TODO: Set poolState to a valid state
      poolState = State.Initialized ;
    }

    /**
        @dev   Checks if the pool is in the valid state (Initialized).
        @return True if the pool is in the valid state, false otherwise.
    */
    function isValidState() public view returns (bool) {
        //TODO
      return poolState == State.Initialized;
    }
}
```
