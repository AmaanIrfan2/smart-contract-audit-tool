(venv) amaanirfan@Amaans-MacBook-Air hardhat-project % slither .
'npx hardhat clean' running (wd: /Users/amaanirfan/Desktop/hardhat-project)
'npx hardhat clean --global' running (wd: /Users/amaanirfan/Desktop/hardhat-project)
'npx hardhat compile --force' running (wd: /Users/amaanirfan/Desktop/hardhat-project)
INFO:Detectors:
VulnerableEnterpriseContract.emergencyWithdraw() (contracts/VulnerablePpxty.sol#50-53) sends eth to arbitrary user
        Dangerous calls:
        - address(msg.sender).transfer(address(this).balance) (contracts/VulnerablePpxty.sol#52)
VulnerableEnterpriseContract.batchTransfer(address[],uint256[]) (contracts/VulnerablePpxty.sol#142-147) sends eth to arbitrary user
        Dangerous calls:
        - recipients[i].call{value: amounts[i]}() (contracts/VulnerablePpxty.sol#145)
VulnerableEnterpriseContract.flashLoan(uint256) (contracts/VulnerablePpxty.sol#155-167) sends eth to arbitrary user
        Dangerous calls:
        - address(msg.sender).transfer(amount) (contracts/VulnerablePpxty.sol#159)
VulnerableEnterpriseContract.lottery() (contracts/VulnerablePpxty.sol#204-216) sends eth to arbitrary user
        Dangerous calls:
        - address(msg.sender).transfer(address(this).balance) (contracts/VulnerablePpxty.sol#214)
VulnerableEnterpriseContract.distributeToAll() (contracts/VulnerablePpxty.sol#219-225) sends eth to arbitrary user
        Dangerous calls:
        - address(users[i]).transfer(1000000000000000000) (contracts/VulnerablePpxty.sol#223)
VulnerableEnterpriseContract.frontRunVulnerable(uint256) (contracts/VulnerablePpxty.sol#321-327) sends eth to arbitrary user
        Dangerous calls:
        - address(msg.sender).transfer(address(this).balance) (contracts/VulnerablePpxty.sol#325)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#functions-that-send-ether-to-arbitrary-destinations
INFO:Detectors:
VulnerableStakingContract.claimRewards() (contracts/VulnerableDS.sol#93-104) uses a weak PRNG: "randomNumber = uint256(blockhash(uint256)(block.number - 1)) % 100 (contracts/VulnerableDS.sol#95)" 
VulnerableEnterpriseContract.getTokenPrice() (contracts/VulnerablePpxty.sol#61-64) uses a weak PRNG: "(block.timestamp % 1000) + 100 (contracts/VulnerablePpxty.sol#63)" 
VulnerableEnterpriseContract.generateRandomNumber() (contracts/VulnerablePpxty.sol#191-202) uses a weak PRNG: "randomNum = uint256(keccak256(bytes)(abi.encodePacked(block.timestamp,block.difficulty,block.coinbase,nonce ++))) % 1000 (contracts/VulnerablePpxty.sol#193-198)" 
VulnerableEnterpriseContract.lottery() (contracts/VulnerablePpxty.sol#204-216) uses a weak PRNG: "winningNumber = uint256(keccak256(bytes)(abi.encodePacked(blockhash(uint256)(block.number - 1),msg.sender))) % 10 (contracts/VulnerablePpxty.sol#208-211)" 
VulnerableEnterpriseContract.weakRandom() (contracts/VulnerablePpxty.sol#245-247) uses a weak PRNG: "uint256(keccak256(bytes)(abi.encodePacked(block.timestamp))) % 100 (contracts/VulnerablePpxty.sol#246)" 
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#weak-PRNG
INFO:Detectors:
VulnerableEnterpriseContract.delegateToContract(address,bytes) (contracts/VulnerablePpxty.sol#149-152) uses delegatecall to a input-controlled function id
        - target.delegatecall(data) (contracts/VulnerablePpxty.sol#151)
VulnerableEnterpriseContract.fallback() (contracts/VulnerablePpxty.sol#287-294) uses delegatecall to a input-controlled function id
        - target.delegatecall(msg.data) (contracts/VulnerablePpxty.sol#291)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#controlled-delegatecall
INFO:Detectors:
Reentrancy in VulnerableEnterpriseContract.complexWithdraw(address) (contracts/VulnerablePpxty.sol#125-134):
        External calls:
        - (success,None) = recipient.call{value: amount / 2}() (contracts/VulnerablePpxty.sol#130)
        External calls sending eth:
        - address(recipient).transfer(amount / 2) (contracts/VulnerablePpxty.sol#129)
        - (success,None) = recipient.call{value: amount / 2}() (contracts/VulnerablePpxty.sol#130)
        State variables written after the call(s):
        - userBalances[msg.sender] = 0 (contracts/VulnerablePpxty.sol#133)
        VulnerableEnterpriseContract.userBalances (contracts/VulnerablePpxty.sol#14) can be used in cross function reentrancies:
        - VulnerableEnterpriseContract.complexWithdraw(address) (contracts/VulnerablePpxty.sol#125-134)
        - VulnerableEnterpriseContract.distributeRewards() (contracts/VulnerablePpxty.sol#77-88)
        - VulnerableEnterpriseContract.setUserBalance(address,uint256) (contracts/VulnerablePpxty.sol#102-105)
        - VulnerableEnterpriseContract.userBalances (contracts/VulnerablePpxty.sol#14)
        - VulnerableEnterpriseContract.withdrawBalance() (contracts/VulnerablePpxty.sol#113-123)
Reentrancy in VulnerableStakingContract.withdraw(uint256) (contracts/VulnerableDS.sol#75-88):
        External calls:
        - (success,None) = msg.sender.call{value: _amount}() (contracts/VulnerableDS.sol#80)
        State variables written after the call(s):
        - balances[msg.sender] -= _amount (contracts/VulnerableDS.sol#84)
        VulnerableStakingContract.balances (contracts/VulnerableDS.sol#12) can be used in cross function reentrancies:
        - VulnerableStakingContract.balances (contracts/VulnerableDS.sol#12)
        - VulnerableStakingContract.claimRewards() (contracts/VulnerableDS.sol#93-104)
        - VulnerableStakingContract.distributeRewards() (contracts/VulnerableDS.sol#149-156)
        - VulnerableStakingContract.receive() (contracts/VulnerableDS.sol#177-182)
        - VulnerableStakingContract.stake(uint256) (contracts/VulnerableDS.sol#57-69)
        - VulnerableStakingContract.withdraw(uint256) (contracts/VulnerableDS.sol#75-88)
Reentrancy in VulnerableEnterpriseContract.withdrawBalance() (contracts/VulnerablePpxty.sol#113-123):
        External calls:
        - (success,None) = msg.sender.call{value: amount}() (contracts/VulnerablePpxty.sol#117)
        State variables written after the call(s):
        - userBalances[msg.sender] = 0 (contracts/VulnerablePpxty.sol#121)
        VulnerableEnterpriseContract.userBalances (contracts/VulnerablePpxty.sol#14) can be used in cross function reentrancies:
        - VulnerableEnterpriseContract.complexWithdraw(address) (contracts/VulnerablePpxty.sol#125-134)
        - VulnerableEnterpriseContract.distributeRewards() (contracts/VulnerablePpxty.sol#77-88)
        - VulnerableEnterpriseContract.setUserBalance(address,uint256) (contracts/VulnerablePpxty.sol#102-105)
        - VulnerableEnterpriseContract.userBalances (contracts/VulnerablePpxty.sol#14)
        - VulnerableEnterpriseContract.withdrawBalance() (contracts/VulnerablePpxty.sol#113-123)
Reentrancy in VulnerableStakingContract.withdrawRewards() (contracts/VulnerableDS.sol#109-120):
        External calls:
        - (success,None) = msg.sender.call{value: reward}() (contracts/VulnerableDS.sol#114)
        State variables written after the call(s):
        - rewards[msg.sender] = 0 (contracts/VulnerableDS.sol#117)
        VulnerableStakingContract.rewards (contracts/VulnerableDS.sol#13) can be used in cross function reentrancies:
        - VulnerableStakingContract.claimRewards() (contracts/VulnerableDS.sol#93-104)
        - VulnerableStakingContract.distributeRewards() (contracts/VulnerableDS.sol#149-156)
        - VulnerableStakingContract.rewards (contracts/VulnerableDS.sol#13)
        - VulnerableStakingContract.withdrawRewards() (contracts/VulnerableDS.sol#109-120)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities
INFO:Detectors:
VulnerableEnterpriseContract.destroy() (contracts/VulnerablePpxty.sol#250-253) allows anyone to destruct the contract
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#suicidal
INFO:Detectors:
VulnerableEnterpriseContract.lottery() (contracts/VulnerablePpxty.sol#204-216) uses a dangerous strict equality:
        - winningNumber == 7 (contracts/VulnerablePpxty.sol#213)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#dangerous-strict-equalities
INFO:Detectors:
VulnerableStakingContract.transferOwnership(address) (contracts/VulnerableDS.sol#132-136) uses tx.origin for authorization: require(bool,string)(tx.origin == owner,Not authorized) (contracts/VulnerableDS.sol#134)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#dangerous-usage-of-txorigin
INFO:Detectors:
VulnerableEnterpriseContract.makeExternalCall(address,bytes) (contracts/VulnerablePpxty.sol#137-140) ignores return value by target.call(data) (contracts/VulnerablePpxty.sol#139)
VulnerableEnterpriseContract.batchTransfer(address[],uint256[]) (contracts/VulnerablePpxty.sol#142-147) ignores return value by recipients[i].call{value: amounts[i]}() (contracts/VulnerablePpxty.sol#145)
VulnerableEnterpriseContract.delegateToContract(address,bytes) (contracts/VulnerablePpxty.sol#149-152) ignores return value by target.delegatecall(data) (contracts/VulnerablePpxty.sol#151)
VulnerableEnterpriseContract.fallback() (contracts/VulnerablePpxty.sol#287-294) ignores return value by target.delegatecall(msg.data) (contracts/VulnerablePpxty.sol#291)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#unchecked-low-level-calls
INFO:Detectors:
VulnerableStakingContract.transferOwnership(address).newOwner (contracts/VulnerableDS.sol#132) lacks a zero-check on :
                - owner = newOwner (contracts/VulnerableDS.sol#135)
VulnerableEnterpriseContract.complexWithdraw(address).recipient (contracts/VulnerablePpxty.sol#125) lacks a zero-check on :
                - address(recipient).transfer(amount / 2) (contracts/VulnerablePpxty.sol#129)
                - (success,None) = recipient.call{value: amount / 2}() (contracts/VulnerablePpxty.sol#130)
VulnerableEnterpriseContract.makeExternalCall(address,bytes).target (contracts/VulnerablePpxty.sol#137) lacks a zero-check on :
                - target.call(data) (contracts/VulnerablePpxty.sol#139)
VulnerableEnterpriseContract.delegateToContract(address,bytes).target (contracts/VulnerablePpxty.sol#149) lacks a zero-check on :
                - target.delegatecall(data) (contracts/VulnerablePpxty.sol#151)
VulnerableEnterpriseContract.fallback().target (contracts/VulnerablePpxty.sol#290) lacks a zero-check on :
                - target.delegatecall(msg.data) (contracts/VulnerablePpxty.sol#291)
VulnerableDelegate.initialize(address)._owner (contracts/VulnerablePpxty.sol#335) lacks a zero-check on :
                - owner = _owner (contracts/VulnerablePpxty.sol#337)
VulnerableUpgradeable.initialize(address)._admin (contracts/VulnerablePpxty.sol#352) lacks a zero-check on :
                - admin = _admin (contracts/VulnerablePpxty.sol#354)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#missing-zero-address-validation
INFO:Detectors:
VulnerableEnterpriseContract.batchTransfer(address[],uint256[]) (contracts/VulnerablePpxty.sol#142-147) has external calls inside a loop: recipients[i].call{value: amounts[i]}() (contracts/VulnerablePpxty.sol#145)
VulnerableEnterpriseContract.distributeToAll() (contracts/VulnerablePpxty.sol#219-225) has external calls inside a loop: address(users[i]).transfer(1000000000000000000) (contracts/VulnerablePpxty.sol#223)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation/#calls-inside-a-loop
INFO:Detectors:
Reentrancy in VulnerableEnterpriseContract.fallback() (contracts/VulnerablePpxty.sol#287-294):
        External calls:
        - target.delegatecall(msg.data) (contracts/VulnerablePpxty.sol#291)
        State variables written after the call(s):
        - totalEtherBalance += msg.value (contracts/VulnerablePpxty.sol#293)
Reentrancy in VulnerableStakingContract.withdraw(uint256) (contracts/VulnerableDS.sol#75-88):
        External calls:
        - (success,None) = msg.sender.call{value: _amount}() (contracts/VulnerableDS.sol#80)
        State variables written after the call(s):
        - totalStaked -= _amount (contracts/VulnerableDS.sol#85)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-2
INFO:Detectors:
Reentrancy in VulnerableStakingContract.withdraw(uint256) (contracts/VulnerableDS.sol#75-88):
        External calls:
        - (success,None) = msg.sender.call{value: _amount}() (contracts/VulnerableDS.sol#80)
        Event emitted after the call(s):
        - Withdrawn(msg.sender,_amount) (contracts/VulnerableDS.sol#87)
Reentrancy in VulnerableEnterpriseContract.withdrawBalance() (contracts/VulnerablePpxty.sol#113-123):
        External calls:
        - (success,None) = msg.sender.call{value: amount}() (contracts/VulnerablePpxty.sol#117)
        Event emitted after the call(s):
        - Withdrawal(msg.sender,amount) (contracts/VulnerablePpxty.sol#122)
Reentrancy in VulnerableStakingContract.withdrawRewards() (contracts/VulnerableDS.sol#109-120):
        External calls:
        - (success,None) = msg.sender.call{value: reward}() (contracts/VulnerableDS.sol#114)
        Event emitted after the call(s):
        - RewardPaid(msg.sender,reward) (contracts/VulnerableDS.sol#119)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-3
INFO:Detectors:
VulnerableStakingContract.withdraw(uint256) (contracts/VulnerableDS.sol#75-88) uses timestamp for comparisons
        Dangerous comparisons:
        - require(bool,string)(block.timestamp >= lockTime[msg.sender],Tokens locked) (contracts/VulnerableDS.sol#77)
VulnerableEnterpriseContract.swapTokens(uint256) (contracts/VulnerablePpxty.sol#66-74) uses timestamp for comparisons
        Dangerous comparisons:
        - require(bool,string)(address(this).balance >= ethAmount,Insufficient contract balance) (contracts/VulnerablePpxty.sol#71)
VulnerableEnterpriseContract.timeBasedFunction() (contracts/VulnerablePpxty.sol#239-242) uses timestamp for comparisons
        Dangerous comparisons:
        - require(bool,string)(block.timestamp > 1640995200,Too early) (contracts/VulnerablePpxty.sol#240)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#block-timestamp
INFO:Detectors:
VulnerableEnterpriseContract.assemblyExample(uint256) (contracts/VulnerablePpxty.sol#301-307) uses assembly
        - INLINE ASM (contracts/VulnerablePpxty.sol#302-306)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#assembly-usage
INFO:Detectors:
6 different versions of Solidity are used:
        - Version constraint ^0.8.20 is used by:
                -^0.8.20 (node_modules/@openzeppelin/contracts/access/Ownable.sol#4)
                -^0.8.20 (node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#4)
                -^0.8.20 (node_modules/@openzeppelin/contracts/utils/Context.sol#4)
        - Version constraint >=0.8.4 is used by:
                ->=0.8.4 (node_modules/@openzeppelin/contracts/interfaces/draft-IERC6093.sol#3)
        - Version constraint >=0.4.16 is used by:
                ->=0.4.16 (node_modules/@openzeppelin/contracts/token/ERC20/IERC20.sol#4)
        - Version constraint >=0.6.2 is used by:
                ->=0.6.2 (node_modules/@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol#4)
        - Version constraint ^0.8.0 is used by:
                -^0.8.0 (contracts/VulnerableDS.sol#2)
        - Version constraint ^0.8.19 is used by:
                -^0.8.19 (contracts/VulnerablePpxty.sol#3)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#different-pragma-directives-are-used
INFO:Detectors:
Version constraint ^0.8.20 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
        - VerbatimInvalidDeduplication
        - FullInlinerNonExpressionSplitArgumentEvaluationOrder
        - MissingSideEffectsOnSelectorAccess.
It is used by:
        - ^0.8.20 (node_modules/@openzeppelin/contracts/access/Ownable.sol#4)
        - ^0.8.20 (node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#4)
        - ^0.8.20 (node_modules/@openzeppelin/contracts/utils/Context.sol#4)
Version constraint >=0.8.4 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
        - FullInlinerNonExpressionSplitArgumentEvaluationOrder
        - MissingSideEffectsOnSelectorAccess
        - AbiReencodingHeadOverflowWithStaticArrayCleanup
        - DirtyBytesArrayToStorage
        - DataLocationChangeInInternalOverride
        - NestedCalldataArrayAbiReencodingSizeValidation
        - SignedImmutables.
It is used by:
        - >=0.8.4 (node_modules/@openzeppelin/contracts/interfaces/draft-IERC6093.sol#3)
Version constraint >=0.4.16 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
        - DirtyBytesArrayToStorage
        - ABIDecodeTwoDimensionalArrayMemory
        - KeccakCaching
        - EmptyByteArrayCopy
        - DynamicArrayCleanup
        - ImplicitConstructorCallvalueCheck
        - TupleAssignmentMultiStackSlotComponents
        - MemoryArrayCreationOverflow
        - privateCanBeOverridden
        - SignedArrayStorageCopy
        - ABIEncoderV2StorageArrayWithMultiSlotElement
        - DynamicConstructorArgumentsClippedABIV2
        - UninitializedFunctionPointerInConstructor_0.4.x
        - IncorrectEventSignatureInLibraries_0.4.x
        - ExpExponentCleanup
        - NestedArrayFunctionCallDecoder
        - ZeroFunctionSelector.
It is used by:
        - >=0.4.16 (node_modules/@openzeppelin/contracts/token/ERC20/IERC20.sol#4)
Version constraint >=0.6.2 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
        - MissingSideEffectsOnSelectorAccess
        - AbiReencodingHeadOverflowWithStaticArrayCleanup
        - DirtyBytesArrayToStorage
        - NestedCalldataArrayAbiReencodingSizeValidation
        - ABIDecodeTwoDimensionalArrayMemory
        - KeccakCaching
        - EmptyByteArrayCopy
        - DynamicArrayCleanup
        - MissingEscapingInFormatting
        - ArraySliceDynamicallyEncodedBaseType
        - ImplicitConstructorCallvalueCheck
        - TupleAssignmentMultiStackSlotComponents
        - MemoryArrayCreationOverflow.
It is used by:
        - >=0.6.2 (node_modules/@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol#4)
Version constraint ^0.8.0 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
        - FullInlinerNonExpressionSplitArgumentEvaluationOrder
        - MissingSideEffectsOnSelectorAccess
        - AbiReencodingHeadOverflowWithStaticArrayCleanup
        - DirtyBytesArrayToStorage
        - DataLocationChangeInInternalOverride
        - NestedCalldataArrayAbiReencodingSizeValidation
        - SignedImmutables
        - ABIDecodeTwoDimensionalArrayMemory
        - KeccakCaching.
It is used by:
        - ^0.8.0 (contracts/VulnerableDS.sol#2)
Version constraint ^0.8.19 contains known severe issues (https://solidity.readthedocs.io/en/latest/bugs.html)
        - VerbatimInvalidDeduplication
        - FullInlinerNonExpressionSplitArgumentEvaluationOrder
        - MissingSideEffectsOnSelectorAccess.
It is used by:
        - ^0.8.19 (contracts/VulnerablePpxty.sol#3)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Low level call in VulnerableStakingContract.withdraw(uint256) (contracts/VulnerableDS.sol#75-88):
        - (success,None) = msg.sender.call{value: _amount}() (contracts/VulnerableDS.sol#80)
Low level call in VulnerableStakingContract.withdrawRewards() (contracts/VulnerableDS.sol#109-120):
        - (success,None) = msg.sender.call{value: reward}() (contracts/VulnerableDS.sol#114)
Low level call in VulnerableEnterpriseContract.withdrawBalance() (contracts/VulnerablePpxty.sol#113-123):
        - (success,None) = msg.sender.call{value: amount}() (contracts/VulnerablePpxty.sol#117)
Low level call in VulnerableEnterpriseContract.complexWithdraw(address) (contracts/VulnerablePpxty.sol#125-134):
        - (success,None) = recipient.call{value: amount / 2}() (contracts/VulnerablePpxty.sol#130)
Low level call in VulnerableEnterpriseContract.makeExternalCall(address,bytes) (contracts/VulnerablePpxty.sol#137-140):
        - target.call(data) (contracts/VulnerablePpxty.sol#139)
Low level call in VulnerableEnterpriseContract.batchTransfer(address[],uint256[]) (contracts/VulnerablePpxty.sol#142-147):
        - recipients[i].call{value: amounts[i]}() (contracts/VulnerablePpxty.sol#145)
Low level call in VulnerableEnterpriseContract.delegateToContract(address,bytes) (contracts/VulnerablePpxty.sol#149-152):
        - target.delegatecall(data) (contracts/VulnerablePpxty.sol#151)
Low level call in VulnerableEnterpriseContract.flashLoan(uint256) (contracts/VulnerablePpxty.sol#155-167):
        - (success,None) = msg.sender.call(abi.encodeWithSignature(onFlashLoan(uint256),amount)) (contracts/VulnerablePpxty.sol#162)
Low level call in VulnerableEnterpriseContract.fallback() (contracts/VulnerablePpxty.sol#287-294):
        - target.delegatecall(msg.data) (contracts/VulnerablePpxty.sol#291)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#low-level-calls
INFO:Detectors:
Parameter VulnerableStakingContract.stake(uint256)._amount (contracts/VulnerableDS.sol#57) is not in mixedCase
Parameter VulnerableStakingContract.withdraw(uint256)._amount (contracts/VulnerableDS.sol#75) is not in mixedCase
Variable VulnerableStakingContract.REWARD_RATE (contracts/VulnerableDS.sol#18) is not in mixedCase
Parameter VulnerableDelegate.initialize(address)._owner (contracts/VulnerablePpxty.sol#335) is not in mixedCase
Parameter VulnerableUpgradeable.initialize(address)._admin (contracts/VulnerablePpxty.sol#352) is not in mixedCase
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#conformance-to-solidity-naming-conventions
INFO:Detectors:
Reentrancy in VulnerableEnterpriseContract.complexWithdraw(address) (contracts/VulnerablePpxty.sol#125-134):
        External calls:
        - address(recipient).transfer(amount / 2) (contracts/VulnerablePpxty.sol#129)
        External calls sending eth:
        - address(recipient).transfer(amount / 2) (contracts/VulnerablePpxty.sol#129)
        - (success,None) = recipient.call{value: amount / 2}() (contracts/VulnerablePpxty.sol#130)
        State variables written after the call(s):
        - userBalances[msg.sender] = 0 (contracts/VulnerablePpxty.sol#133)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-4
INFO:Detectors:
VulnerableEnterpriseContract.slitherConstructorConstantVariables() (contracts/VulnerablePpxty.sol#9-328) uses literals with too many digits:
        - INITIAL_SUPPLY = 1000000 * 10 ** 18 (contracts/VulnerablePpxty.sol#13)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#too-many-digits
INFO:Detectors:
VulnerableStakingContract.MAX_UINT (contracts/VulnerableDS.sol#20) is never used in VulnerableStakingContract (contracts/VulnerableDS.sol#9-184)
VulnerableEnterpriseContract.secretBalances (contracts/VulnerablePpxty.sol#16) is never used in VulnerableEnterpriseContract (contracts/VulnerablePpxty.sol#9-328)
VulnerableEnterpriseContract.ownerBalance (contracts/VulnerablePpxty.sol#280) is never used in VulnerableEnterpriseContract (contracts/VulnerablePpxty.sol#9-328)
VulnerableEnterpriseContract.unusedVariable (contracts/VulnerablePpxty.sol#283) is never used in VulnerableEnterpriseContract (contracts/VulnerablePpxty.sol#9-328)
VulnerableEnterpriseContract.unusedAddress (contracts/VulnerablePpxty.sol#284) is never used in VulnerableEnterpriseContract (contracts/VulnerablePpxty.sol#9-328)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#unused-state-variable
INFO:Detectors:
Loop condition i < stakeholders.length (contracts/VulnerableDS.sol#151) should use cached array length instead of referencing `length` member of the storage array.
 Loop condition i < users.length (contracts/VulnerablePpxty.sol#221) should use cached array length instead of referencing `length` member of the storage array.
 Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#cache-array-length
INFO:Detectors:
VulnerableEnterpriseContract.ownerBalance (contracts/VulnerablePpxty.sol#280) should be constant 
VulnerableEnterpriseContract.unusedAddress (contracts/VulnerablePpxty.sol#284) should be constant 
VulnerableEnterpriseContract.unusedVariable (contracts/VulnerablePpxty.sol#283) should be constant 
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#state-variables-that-could-be-declared-constant
INFO:Slither:. analyzed (12 contracts with 100 detectors), 75 result(s) found
(venv) amaanirfan@Amaans-MacBook-Air hardhat-project % 

This is the slither output, explain this to me, is it able to detect all the errors correctly? 