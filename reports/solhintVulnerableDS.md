
Solhint is a linter, used for coding standards, style, documentation & basic security lint. It doesnt detect logic flaws or other vulnerabilities. Following is the report.


contracts/VulnerableDS.sol
    2:1   error    Compiler version ^0.8.0 does not satisfy the ^0.8.24 semver requirement                                compiler-version
    9:1   warning  Missing @author tag in contract 'VulnerableStakingContract'                                            use-natspec
    9:1   warning  Missing @notice tag in contract 'VulnerableStakingContract'                                            use-natspec
   12:5   warning  Missing @notice tag in variable 'balances'                                                             use-natspec
   13:5   warning  Missing @notice tag in variable 'rewards'                                                              use-natspec
   14:5   warning  Missing @notice tag in variable 'lockTime'                                                             use-natspec
   16:5   warning  Missing @notice tag in variable 'owner'                                                                use-natspec
   17:5   warning  Missing @notice tag in variable 'totalStaked'                                                          use-natspec
   18:5   warning  Missing @notice tag in variable 'REWARD_RATE'                                                          use-natspec
   18:5   warning  Variable name must be in mixedCase REWARD_RATE                                                         var-name-mixedcase
   24:5   warning  Missing @notice tag in event 'Staked'                                                                  use-natspec
   24:5   warning  Missing @param tag in event 'Staked'                                                                   use-natspec
   24:5   warning  Mismatch in @param names for event 'Staked'. Expected: [user, amount], Found: []                       use-natspec
   24:5   warning  GC: [amount] on Event [Staked] could be Indexed                                                        gas-indexed-events
   25:5   warning  Missing @notice tag in event 'Withdrawn'                                                               use-natspec
   25:5   warning  Missing @param tag in event 'Withdrawn'                                                                use-natspec
   25:5   warning  Mismatch in @param names for event 'Withdrawn'. Expected: [user, amount], Found: []                    use-natspec
   25:5   warning  GC: [amount] on Event [Withdrawn] could be Indexed                                                     gas-indexed-events
   26:5   warning  Missing @notice tag in event 'RewardPaid'                                                              use-natspec
   26:5   warning  Missing @param tag in event 'RewardPaid'                                                               use-natspec
   26:5   warning  Mismatch in @param names for event 'RewardPaid'. Expected: [user, reward], Found: []                   use-natspec
   26:5   warning  GC: [reward] on Event [RewardPaid] could be Indexed                                                    gas-indexed-events
   31:9   warning  GC: Use Custom Errors instead of require statements                                                    gas-custom-errors
   37:9   warning  GC: Use Custom Errors instead of require statements                                                    gas-custom-errors
   45:5   warning  Missing @notice tag in function '<anonymous>'                                                          use-natspec
   45:5   warning  Explicitly mark visibility in function (Set ignoreConstructors to true if using solidity >=0.7.0)      func-visibility
   57:5   warning  Missing @notice tag in function 'stake'                                                                use-natspec
   75:5   warning  Missing @notice tag in function 'withdraw'                                                             use-natspec
   76:9   warning  GC: Use Custom Errors instead of require statements                                                    gas-custom-errors
   76:17  warning  GC: Non strict inequality found. Try converting to a strict one                                        gas-strict-inequalities
   77:9   warning  GC: Use Custom Errors instead of require statements                                                    gas-custom-errors
   77:17  warning  GC: Non strict inequality found. Try converting to a strict one                                        gas-strict-inequalities
   81:9   warning  GC: Use Custom Errors instead of require statements                                                    gas-custom-errors
   93:5   warning  Missing @notice tag in function 'claimRewards'                                                         use-natspec
  109:5   warning  Missing @notice tag in function 'withdrawRewards'                                                      use-natspec
  111:9   warning  GC: Use Custom Errors instead of require statements                                                    gas-custom-errors
  114:10  warning  Variable "success" is unused                                                                           no-unused-vars
  125:5   warning  Missing @notice tag in function 'addFunds'                                                             use-natspec
  125:52  warning  Code contains empty blocks                                                                             no-empty-blocks
  132:5   warning  Missing @notice tag in function 'transferOwnership'                                                    use-natspec
  132:5   warning  Missing @param tag in function 'transferOwnership'                                                     use-natspec
  132:5   warning  Mismatch in @param names for function 'transferOwnership'. Expected: [newOwner], Found: []             use-natspec
  134:9   warning  GC: Use Custom Errors instead of require statements                                                    gas-custom-errors
  134:17  warning  Avoid to use tx.origin                                                                                 avoid-tx-origin
  141:5   warning  Missing @notice tag in function 'calculatePercentage'                                                  use-natspec
  141:5   warning  Missing @param tag in function 'calculatePercentage'                                                   use-natspec
  141:5   warning  Mismatch in @param names for function 'calculatePercentage'. Expected: [value, percentage], Found: []  use-natspec
  141:5   warning  Missing @return tag in function 'calculatePercentage'                                                  use-natspec
  141:5   warning  Mismatch in @return count for function 'calculatePercentage'. Expected: 1, Found: 0                    use-natspec
  149:5   warning  Missing @notice tag in function 'distributeRewards'                                                    use-natspec
  151:54  warning  GC: For [ i ] variable, increment/decrement by 1 using: [ ++variable ] to save gas                     gas-increment-by-one
  161:5   warning  Missing @notice tag in function 'emergencyShutdown'                                                    use-natspec
  169:5   warning  Missing @notice tag in function 'updateRewardRate'                                                     use-natspec
  169:5   warning  Missing @param tag in function 'updateRewardRate'                                                      use-natspec
  169:5   warning  Mismatch in @param names for function 'updateRewardRate'. Expected: [newRate], Found: []               use-natspec
  177:5   warning  Missing @notice tag in function '<anonymous>'                                                          use-natspec

✖ 56 problems (1 error, 55 warnings)

 -------------------------------------------------------------------------- 
 ===> Join SOLHINT Community at: https://discord.com/invite/4TYGq3zpjs <=== 
 -------------------------------------------------------------------------- 