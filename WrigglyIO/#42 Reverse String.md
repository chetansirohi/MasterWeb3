### Here we have two functions, setMessage and reverseMessage. Your job is to ensure _newMessage is not an empty string and then initialize message. Your next task is to reverse the string message.

```
Example 1:

  Input: Reverse this string
  Output: gnirts siht esreveR
  Explanation: This is the reversed string

Constraints:
  
  Ensure _newMessaeg is not an empty string
  Reverse the string message

Hints

  Use require to ensure _newMessage isn't empty
  Use bytes to deal with message and reversing it.
```

### Solution

```
pragma solidity ^0.8.0;

contract StringManipulation {
    
    string public message;
    
    function setMessage(string memory _newMessage) public {
        // TODO: ensure _newMessage is not an empty string
        // TODO: set message
      require(bytes(_newMessage).length != 0,"Invalid String");
      message =_newMessage;
    }
    
    function reverseMessage() public view returns (string memory) {
        // TODO: add code here to reverse the order of characters in the `message` string
        bytes memory ogStr = bytes(message);
        bytes memory reverseStr = new bytes(ogStr.length);
        
        for (uint256 i = 0; i < ogStr.length; i++) {
            reverseStr[i] = ogStr[ogStr.length - 1 - i];
        }
        
        return string(reverseStr);
    }
}
```
