### Create a Solidity contract called Crowdfunding that allows users to donate funds to a project and tracks the total amount raised. Ensure that only the owner can withdrawFunds

Example 1:

  Input: 1500000000000000000
  Output: 1500000000000000000
  Explanation: 1.5 ether is donated and total raised is set to 1500000000000000000 wei.
  
Constraints:

The value will be passed through the msg and therefore does not need to be passed to `donate`.

Hints

  Set the contract creator as the owner in the constructor.
  Update the donate() function to update the totalRaised variable with the amount of ether donated.
  Allow the owner to withdraw the entire balance of the contract in the withdrawFunds() function.
