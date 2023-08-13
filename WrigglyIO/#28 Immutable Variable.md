### Immutable variables are like constants. Values of immutable variables can be set inside the constructor but cannot be modified afterwards. Currently we are setting the immutable variables in a setter function. However, this is not allowed as they can only be initialized inside a constructor. Fix the bug.

```
Example 1:

  Input: 256
  Output: {"0": "address: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4", "1": "uint256: 256"}
  
Constraints:

  The variables should be set inside of the constructor as they are immutable.

Hints

  Remove the setVar function and use a constructor instead to initialize the two variables.

```

### Solution 
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Immutable {
    // coding convention to uppercase constant variables
    address public immutable MY_ADDRESS;
    uint public immutable MY_UINT;

    constructor(uint _myUint){
      MY_ADDRESS = msg.sender;
        MY_UINT = _myUint;
    }

    function setVar() public {
        
    }

    function getVar() public view returns (address, uint) {
        return (MY_ADDRESS, MY_UINT);
    }
}
```
