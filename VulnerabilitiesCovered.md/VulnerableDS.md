Complete Vulnerability Breakdown

1. Reentrancy (3 instances):

   withdraw() function performs external call before updating state
   withdrawRewards() has unchecked external call with state changes after
   receive() function creates potential reentrancy entry point

2. Integer Overflow/Underflow (6 instances):

   stake() function: balances[msg.sender] += _amount
   stake() function: totalStaked += _amount
   withdraw() function: balances[msg.sender] -= _amount
   withdraw() function: totalStaked -= _amount
   calculatePercentage() function: value * percentage overflow potential
   Constructor mentions potential overflow with totalStaked initialization

3. Access Control (2 instances):

   updateRewardRate() missing onlyOwner modifier
   onlyOwner modifier implementation weakness

4. tx.origin Authentication (1 instance):
   
   transferOwnership() uses tx.origin instead of msg.sender

5. Denial of Service (2 instances):

   stake() function with unbounded stakeholders array growth
   distributeRewards() with unbounded loop over stakeholders

6. State Consistency Issues (2 instances):

   withdraw() changes state after external call
   withdrawRewards() changes state after external call

7. Timestamp Dependence (1 instance):  

   stake() function relies on block.timestamp for lock timing
   
8. Insecure Randomness (1 instance):

   claimRewards() uses blockhash for pseudo-randomness

9. Front-running (1 instance):

   claimRewards() has transparent reward calculation vulnerable to MEV

10. Logic Errors (1 instance):

   claimRewards() has flawed reward calculation using random multiplier

11. Unchecked External Calls (1 instance):

   withdrawRewards() doesn't verify call success properly

12. Deprecated Functions (1 instance):

   emergencyShutdown() uses deprecated selfdestruct