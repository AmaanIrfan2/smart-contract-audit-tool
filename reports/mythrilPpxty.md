# Analysis results for contracts/VulnerablePpxty_flat.sol

## Unchecked return value from external call.
- SWC ID: 104
- Severity: Medium
- Contract: VulnerableEnterpriseContract
- Function name: `fallback`
- PC address: 805
- Estimated Gas Usage: 8030 - 64993

### Description

The return value of a message call is not checked.
External calls return a boolean value. If the callee halts with an exception, 'false' is returned and execution continues in the caller. The caller should check whether an exception happened and react accordingly to avoid unexpected behavior. For example it is often desirable to wrap external calls in require() so the transaction is reverted if the call fails.
In file: contracts/VulnerablePpxty_flat.sol:1011

### Code

```
target.delegatecall(msg.data[20:])
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [SOMEGUY], function: unknown, txdata: 0x8319800000000000000000000000000100000000, decoded_data: , value: 0x0


## State access after external call
- SWC ID: 107
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `fallback`
- PC address: 867
- Estimated Gas Usage: 8030 - 64993

### Description

Read of persistent state following external call
The contract account state is accessed after an external call to a fixed address. To prevent reentrancy issues, consider accessing the state only before the call, especially if the callee is untrusted. Alternatively, a reentrancy lock can be used to prevent untrusted callees from re-entering the contract in an intermediate state.
In file: contracts/VulnerablePpxty_flat.sol:1013

### Code

```
totalEtherBalance += msg.value
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [SOMEGUY], function: unknown, txdata: 0x8319800000010108040008102002800100000000, decoded_data: , value: 0x0


## State access after external call
- SWC ID: 107
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `fallback`
- PC address: 883
- Estimated Gas Usage: 8028 - 64991

### Description

Write to persistent state following external call
The contract account state is accessed after an external call to a fixed address. To prevent reentrancy issues, consider accessing the state only before the call, especially if the callee is untrusted. Alternatively, a reentrancy lock can be used to prevent untrusted callees from re-entering the contract in an intermediate state.
In file: contracts/VulnerablePpxty_flat.sol:1013

### Code

```
totalEtherBalance += msg.value
```

### Initial State:

Account: [CREATOR], balance: 0x1, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [CREATOR], function: unknown, txdata: 0xe900200100000000000000000000000000000000, decoded_data: , value: 0x0


## Integer Arithmetic Bugs
- SWC ID: 101
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `constructor`
- PC address: 1397
- Estimated Gas Usage: 53527 - 219543

### Description

The arithmetic operator can underflow.
It is possible to cause an integer overflow or underflow in the arithmetic operation.
In file: #utility.yul:27

### Code

```
_address(offset, end) -> value {
     
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0


## Integer Arithmetic Bugs
- SWC ID: 101
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `assemblyExample(uint256)`
- PC address: 3179
- Estimated Gas Usage: 460 - 650

### Description

The arithmetic operator can overflow.
It is possible to cause an integer overflow or underflow in the arithmetic operation.
In file: contracts/VulnerablePpxty_flat.sol:1023

### Code

```
add(x, 1)
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [CREATOR], function: assemblyExample(uint256), txdata: 0x2c964371ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff, decoded_data: (115792089237316195423570985008687907853269984665640564039457584007913129639935,), value: 0x0


## Integer Arithmetic Bugs
- SWC ID: 101
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `unsafeAdd(uint256,uint256)`
- PC address: 3305
- Estimated Gas Usage: 926 - 1302

### Description

The arithmetic operator can overflow.
It is possible to cause an integer overflow or underflow in the arithmetic operation.
In file: contracts/VulnerablePpxty_flat.sol:893

### Code

```
a + b
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: unsafeAdd(uint256,uint256), txdata: 0x3f3f7899000000010000000000000000deadbeefdeadbeefdeadbeefdeadbeefdeadbeefffffffff00580000000020010000000000000000000000000000000000000000, decoded_data: (26959946667150639795938285700019672329454592770672848370170504003311, 115792089210392449856681423721031216740354224545902874250467730324858513391616), value: 0x0


## Unprotected Ether Withdrawal
- SWC ID: 105
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `frontRunVulnerable(uint256)`
- PC address: 3573
- Estimated Gas Usage: 1319 - 35600

### Description

Any sender can withdraw Ether from the contract account.
Arbitrary senders other than the contract creator can profitably extract Ether from the contract account. Verify the business logic carefully and make sure that appropriate security controls are in place to prevent unexpected loss of funds.
In file: contracts/VulnerablePpxty_flat.sol:1045

### Code

```
payable(msg.sender).transfer(address(this).balance)
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x46ee75cd3e26fffff, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: frontRunVulnerable(uint256), txdata: 0x5ce7aee00000000000000000000000000000000000000000000000000de0b6b3a7640001, decoded_data: (1000000000000000001,), value: 0xde0b6b3a7640001


## External Call To User-Supplied Address
- SWC ID: 107
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `withdrawBalance()`
- PC address: 3712
- Estimated Gas Usage: 8638 - 64119

### Description

A call to a user-supplied address is executed.
An external message call to an address specified by the caller is executed. Note that the callee account might contain arbitrary code and could re-enter any function within this contract. Reentering the contract in an intermediate state may lead to unexpected behaviour. Make sure that no state modifications are executed after this call and/or reentrancy guards are in place.
In file: contracts/VulnerablePpxty_flat.sol:837

### Code

```
msg.sender.call{value: amount}("")
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: withdrawBalance(), txdata: 0x5fd8c710, value: 0x0


## Transaction Order Dependence
- SWC ID: 114
- Severity: Medium
- Contract: VulnerableEnterpriseContract
- Function name: `withdrawBalance()`
- PC address: 3712
- Estimated Gas Usage: 8638 - 64119

### Description

The value of the call is dependent on balance or storage write
This can lead to race conditions. An attacker may be able to run a transaction after our transaction which can change the value of the call
In file: contracts/VulnerablePpxty_flat.sol:837

### Code

```
msg.sender.call{value: amount}("")
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: withdrawBalance(), txdata: 0x5fd8c710, value: 0x0


## State access after external call
- SWC ID: 107
- Severity: Medium
- Contract: VulnerableEnterpriseContract
- Function name: `withdrawBalance()`
- PC address: 3896
- Estimated Gas Usage: 8638 - 64119

### Description

Write to persistent state following external call
The contract account state is accessed after an external call to a user defined address. To prevent reentrancy issues, consider accessing the state only before the call, especially if the callee is untrusted. Alternatively, a reentrancy lock can be used to prevent untrusted callees from re-entering the contract in an intermediate state.
In file: contracts/VulnerablePpxty_flat.sol:841

### Code

```
userBalances[msg.sender] = 0
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: withdrawBalance(), txdata: 0x5fd8c710, value: 0x0


## Unprotected Selfdestruct
- SWC ID: 106
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `destroy()`
- PC address: 4763
- Estimated Gas Usage: 188 - 283

### Description

Any sender can cause the contract to self-destruct.
Any sender can trigger execution of the SELFDESTRUCT instruction to destroy this contract account and withdraw its balance to an arbitrary address. Review the transaction trace generated for this issue and make sure that appropriate security controls are in place to prevent unrestricted access.
In file: contracts/VulnerablePpxty_flat.sol:972

### Code

```
selfdestruct(payable(msg.sender))
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: destroy(), txdata: 0x83197ef0, value: 0x0


## External Call To User-Supplied Address
- SWC ID: 107
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `makeExternalCall(address,bytes)`
- PC address: 5676
- Estimated Gas Usage: 1866 - 38829

### Description

A call to a user-supplied address is executed.
An external message call to an address specified by the caller is executed. Note that the callee account might contain arbitrary code and could re-enter any function within this contract. Reentering the contract in an intermediate state may lead to unexpected behaviour. Make sure that no state modifications are executed after this call and/or reentrancy guards are in place.
In file: contracts/VulnerablePpxty_flat.sol:859

### Code

```
target.call(data)
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [SOMEGUY], function: makeExternalCall(address,bytes), txdata: 0x9cdfbdb5000000000000000000000000deadbeefdeadbeefdeadbeefdeadbeefdeadbeef00000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000000, decoded_data: ('0xdeadbeefdeadbeefdeadbeefdeadbeefdeadbeef', ''), value: 0x0


## Unchecked return value from external call.
- SWC ID: 104
- Severity: Medium
- Contract: VulnerableEnterpriseContract
- Function name: `makeExternalCall(address,bytes)`
- PC address: 5676
- Estimated Gas Usage: 1866 - 38829

### Description

The return value of a message call is not checked.
External calls return a boolean value. If the callee halts with an exception, 'false' is returned and execution continues in the caller. The caller should check whether an exception happened and react accordingly to avoid unexpected behavior. For example it is often desirable to wrap external calls in require() so the transaction is reverted if the call fails.
In file: contracts/VulnerablePpxty_flat.sol:859

### Code

```
target.call(data)
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [CREATOR], function: makeExternalCall(address,bytes), txdata: 0x9cdfbdb500000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005, decoded_data: ('0x0000000000000000000000000000000000000000', ''), value: 0x0


## Integer Arithmetic Bugs
- SWC ID: 101
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `unsafeSub(uint256,uint256)`
- PC address: 5851
- Estimated Gas Usage: 859 - 1235

### Description

The arithmetic operator can underflow.
It is possible to cause an integer overflow or underflow in the arithmetic operation.
In file: contracts/VulnerablePpxty_flat.sol:899

### Code

```
a - b
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [SOMEGUY], function: unsafeSub(uint256,uint256), txdata: 0x9eb4547b000000000000000000000000aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa000000000100000000000001aaaaaaaaaaaaabaaabababaaaaaaaaaaaaaaabab, decoded_data: (974334424887268612135789888477522013103955028650, 105312291668557189133754089901841982941090118904032010528994536363), value: 0x0


## Delegatecall to user-supplied address
- SWC ID: 112
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `delegateToContract(address,bytes)`
- PC address: 5909
- Estimated Gas Usage: 1930 - 38893

### Description

The contract delegates execution to another contract with a user-supplied address.
The smart contract delegates execution to a user-supplied address.This could allow an attacker to execute arbitrary code in the context of this contract account and manipulate the state of the contract account or execute actions on its behalf.
In file: contracts/VulnerablePpxty_flat.sol:871

### Code

```
target.delegatecall(data)
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: delegateToContract(address,bytes), txdata: 0x9f07922e000000000000000000000000deadbeefdeadbeefdeadbeefdeadbeefdeadbeef00000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000000, decoded_data: ('0xdeadbeefdeadbeefdeadbeefdeadbeefdeadbeef', '0000000000000000000000000000000000000000000000000000000000000000'), value: 0x0


## Unchecked return value from external call.
- SWC ID: 104
- Severity: Medium
- Contract: VulnerableEnterpriseContract
- Function name: `delegateToContract(address,bytes)`
- PC address: 5909
- Estimated Gas Usage: 1930 - 38893

### Description

The return value of a message call is not checked.
External calls return a boolean value. If the callee halts with an exception, 'false' is returned and execution continues in the caller. The caller should check whether an exception happened and react accordingly to avoid unexpected behavior. For example it is often desirable to wrap external calls in require() so the transaction is reverted if the call fails.
In file: contracts/VulnerablePpxty_flat.sol:871

### Code

```
target.delegatecall(data)
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [CREATOR], function: delegateToContract(address,bytes), txdata: 0x9f07922e0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000e, decoded_data: ('0x0000000000000000000000000000000000000000', ''), value: 0x0


## Integer Arithmetic Bugs
- SWC ID: 101
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `lottery()`
- PC address: 6156
- Estimated Gas Usage: 1201 - 1955

### Description

The arithmetic operator can underflow.
It is possible to cause an integer overflow or underflow in the arithmetic operation.
In file: contracts/VulnerablePpxty_flat.sol:933

### Code

```
winningNumber == 7
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x2, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: lottery(), txdata: 0xba13a572, value: 0x1


## Dependence on predictable environment variable
- SWC ID: 120
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `lottery()`
- PC address: 6160
- Estimated Gas Usage: 1179 - 1933

### Description

A control flow decision is made based on The block hash of a previous block.
The block hash of a previous block is used to determine a control flow decision. Note that the values of variables like coinbase, gaslimit, block number and timestamp are predictable and can be manipulated by a malicious miner. Also keep in mind that attackers know hashes of earlier blocks. Don't use any of those environment variables as sources of randomness and be aware that use of these variables introduces a certain level of trust into miners.
In file: contracts/VulnerablePpxty_flat.sol:933

### Code

```
if (winningNumber == 7) {
            payable(msg.sender).transfer(address(this).balance);
        }
```

### Initial State:

Account: [CREATOR], balance: 0x2, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [CREATOR], function: lottery(), txdata: 0xba13a572, value: 0x1


## Transaction Order Dependence
- SWC ID: 114
- Severity: Medium
- Contract: VulnerableEnterpriseContract
- Function name: `complexWithdraw(address)`
- PC address: 6453
- Estimated Gas Usage: 8772 - 97902

### Description

The value of the call is dependent on balance or storage write
This can lead to race conditions. An attacker may be able to run a transaction after our transaction which can change the value of the call
In file: contracts/VulnerablePpxty_flat.sol:849

### Code

```
payable(recipient).transfer(amount / 2)
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x40000400040a9, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: complexWithdraw(address), txdata: 0xbd239b010000000000000000000000000901d12ebe1b195e5aa8748e62bd7734ae19b51f, decoded_data: ('0x0901d12ebe1b195e5aa8748e62bd7734ae19b51f',), value: 0x0


## External Call To User-Supplied Address
- SWC ID: 107
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `complexWithdraw(address)`
- PC address: 6535
- Estimated Gas Usage: 8772 - 97902

### Description

A call to a user-supplied address is executed.
An external message call to an address specified by the caller is executed. Note that the callee account might contain arbitrary code and could re-enter any function within this contract. Reentering the contract in an intermediate state may lead to unexpected behaviour. Make sure that no state modifications are executed after this call and/or reentrancy guards are in place.
In file: contracts/VulnerablePpxty_flat.sol:850

### Code

```
recipient.call{value: amount / 2}("")
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: complexWithdraw(address), txdata: 0xbd239b01000000000000000000000000deadbeefdeadbeefdeadbeefdeadbeefdeadbeef, decoded_data: ('0xdeadbeefdeadbeefdeadbeefdeadbeefdeadbeef',), value: 0x0


## Multiple Calls in a Single Transaction
- SWC ID: 113
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `complexWithdraw(address)`
- PC address: 6535
- Estimated Gas Usage: 8772 - 97902

### Description

Multiple calls are executed in the same transaction.
This call is executed following another call within the same transaction. It is possible that the call never gets executed if a prior call fails permanently. This might be caused intentionally by a malicious callee. If possible, refactor the code such that each transaction only executes one external call or make sure that all callees can be trusted (i.e. they’re part of your own codebase).
In file: contracts/VulnerablePpxty_flat.sol:850

### Code

```
recipient.call{value: amount / 2}("")
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [CREATOR], function: complexWithdraw(address), txdata: 0xbd239b010000000000000000000000000000000000000000000000000000000000000000, decoded_data: ('0x0000000000000000000000000000000000000000',), value: 0x0


## Transaction Order Dependence
- SWC ID: 114
- Severity: Medium
- Contract: VulnerableEnterpriseContract
- Function name: `complexWithdraw(address)`
- PC address: 6535
- Estimated Gas Usage: 8772 - 97902

### Description

The value of the call is dependent on balance or storage write
This can lead to race conditions. An attacker may be able to run a transaction after our transaction which can change the value of the call
In file: contracts/VulnerablePpxty_flat.sol:850

### Code

```
recipient.call{value: amount / 2}("")
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: complexWithdraw(address), txdata: 0xbd239b010000000000000000000000000000000000000000000000000000000000000000, decoded_data: ('0x0000000000000000000000000000000000000000',), value: 0x0


## State access after external call
- SWC ID: 107
- Severity: Medium
- Contract: VulnerableEnterpriseContract
- Function name: `complexWithdraw(address)`
- PC address: 6719
- Estimated Gas Usage: 8772 - 97902

### Description

Write to persistent state following external call
The contract account state is accessed after an external call to a user defined address. To prevent reentrancy issues, consider accessing the state only before the call, especially if the callee is untrusted. Alternatively, a reentrancy lock can be used to prevent untrusted callees from re-entering the contract in an intermediate state.
In file: contracts/VulnerablePpxty_flat.sol:853

### Code

```
userBalances[msg.sender] = 0
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: complexWithdraw(address), txdata: 0xbd239b01000000000000000000000000deadbeefdeadbeefdeadbeefdeadbeefdeadbeef, decoded_data: ('0xdeadbeefdeadbeefdeadbeefdeadbeefdeadbeef',), value: 0x0


## Unprotected Ether Withdrawal
- SWC ID: 105
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `emergencyWithdraw()`
- PC address: 6772
- Estimated Gas Usage: 1058 - 35339

### Description

Any sender can withdraw Ether from the contract account.
Arbitrary senders other than the contract creator can profitably extract Ether from the contract account. Verify the business logic carefully and make sure that appropriate security controls are in place to prevent unexpected loss of funds.
In file: contracts/VulnerablePpxty_flat.sol:772

### Code

```
payable(msg.sender).transfer(address(this).balance)
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x2256d8014000, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: emergencyWithdraw(), txdata: 0xdb2e21bc, value: 0x0


## Dependence on predictable environment variable
- SWC ID: 116
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `timeBasedFunction()`
- PC address: 7013
- Estimated Gas Usage: 211 - 306

### Description

A control flow decision is made based on The block.timestamp environment variable.
The block.timestamp environment variable is used to determine a control flow decision. Note that the values of variables like coinbase, gaslimit, block number and timestamp are predictable and can be manipulated by a malicious miner. Also keep in mind that attackers know hashes of earlier blocks. Don't use any of those environment variables as sources of randomness and be aware that use of these variables introduces a certain level of trust into miners.
In file: contracts/VulnerablePpxty_flat.sol:960

### Code

```
require(block.timestamp > 1640995200, "Too early")
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [SOMEGUY], function: timeBasedFunction(), txdata: 0xeac50e2b, value: 0x0


## Dependence on predictable environment variable
- SWC ID: 116
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `swapTokens(uint256)`
- PC address: 7329
- Estimated Gas Usage: 1222 - 1317

### Description

A control flow decision is made based on The block.timestamp environment variable.
The block.timestamp environment variable is used to determine a control flow decision. Note that the values of variables like coinbase, gaslimit, block number and timestamp are predictable and can be manipulated by a malicious miner. Also keep in mind that attackers know hashes of earlier blocks. Don't use any of those environment variables as sources of randomness and be aware that use of these variables introduces a certain level of trust into miners.
In file: contracts/VulnerablePpxty_flat.sol:791

### Code

```
require(address(this).balance >= ethAmount, "Insufficient contract balance")
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [CREATOR], function: swapTokens(uint256), txdata: 0xfe784eaa000000000000000000000000000000010950040202c400000200000000000000, decoded_data: (352660883920636151645432954300489793536,), value: 0x0


## Dependence on predictable environment variable
- SWC ID: 116
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `getTokenPrice()`
- PC address: 9591
- Estimated Gas Usage: 539 - 634

### Description

A control flow decision is made based on The block.timestamp environment variable.
The block.timestamp environment variable is used to determine a control flow decision. Note that the values of variables like coinbase, gaslimit, block number and timestamp are predictable and can be manipulated by a malicious miner. Also keep in mind that attackers know hashes of earlier blocks. Don't use any of those environment variables as sources of randomness and be aware that use of these variables introduces a certain level of trust into miners.
In file: #utility.yul:16

### Code

```
fffffffffffffffffffffffffffff)
    }
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: getTokenPrice(), txdata: 0x4b94f50e, value: 0x0


## Integer Arithmetic Bugs
- SWC ID: 101
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `name()`
- PC address: 11796
- Estimated Gas Usage: 3567 - 4792

### Description

The arithmetic operator can underflow.
It is possible to cause an integer overflow or underflow in the arithmetic operation.
In file: #utility.yul:81

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: name(), txdata: 0x06fdde03, value: 0x0


## Integer Arithmetic Bugs
- SWC ID: 101
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `symbol()`
- PC address: 11796
- Estimated Gas Usage: 3654 - 4879

### Description

The arithmetic operator can underflow.
It is possible to cause an integer overflow or underflow in the arithmetic operation.
In file: #utility.yul:81

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [SOMEGUY], function: symbol(), txdata: 0x95d89b41, value: 0x0


## Dependence on predictable environment variable
- SWC ID: 116
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `swapTokens(uint256)`
- PC address: 12015
- Estimated Gas Usage: 1171 - 1266

### Description

A control flow decision is made based on The block.timestamp environment variable.
The block.timestamp environment variable is used to determine a control flow decision. Note that the values of variables like coinbase, gaslimit, block number and timestamp are predictable and can be manipulated by a malicious miner. Also keep in mind that attackers know hashes of earlier blocks. Don't use any of those environment variables as sources of randomness and be aware that use of these variables introduces a certain level of trust into miners.
In file: #utility.yul:81

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: swapTokens(uint256), txdata: 0xfe784eaa0000000000000000000000000000000000000000000000000000000000000000, decoded_data: (0,), value: 0x0


## Integer Arithmetic Bugs
- SWC ID: 101
- Severity: High
- Contract: VulnerableEnterpriseContract
- Function name: `expensiveLoop(uint256)`
- PC address: 12434
- Estimated Gas Usage: 1111 - 1865

### Description

The arithmetic operator can underflow.
It is possible to cause an integer overflow or underflow in the arithmetic operation.
In file: #utility.yul:81

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [SOMEGUY], function: expensiveLoop(uint256), txdata: 0xe81adc400000000000000000000000000000000000000000000000000000000000000001, decoded_data: (1,), value: 0x0


## Dependence on predictable environment variable
- SWC ID: 120
- Severity: Low
- Contract: VulnerableEnterpriseContract
- Function name: `lottery()`
- PC address: 13073
- Estimated Gas Usage: 338 - 433

### Description

A control flow decision is made based on The block.number environment variable.
The block.number environment variable is used to determine a control flow decision. Note that the values of variables like coinbase, gaslimit, block number and timestamp are predictable and can be manipulated by a malicious miner. Also keep in mind that attackers know hashes of earlier blocks. Don't use any of those environment variables as sources of randomness and be aware that use of these variables introduces a certain level of trust into miners.
In file: #utility.yul:81

### Initial State:

Account: [CREATOR], balance: 0x2, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [CREATOR], function: lottery(), txdata: 0xba13a572, value: 0x1


## Exception State
- SWC ID: 110
- Severity: Medium
- Contract: VulnerableEnterpriseContract
- Function name: `assertExample(uint256)`
- PC address: 13394
- Estimated Gas Usage: 536 - 821

### Description

An assertion violation was triggered.
It is possible to trigger an assertion violation. Note that Solidity assert() statements should only be used to check invariants. Review the transaction trace generated for this issue and either make sure your program logic is correct, or use require() instead of assert() if your goal is to constrain user inputs or enforce preconditions. Remember to validate inputs from both callers (for instance, via passed arguments) and callees (for instance, via return values).
In file: contracts/VulnerablePpxty_flat.sol:987

### Code

```
assert(value != 0)
```

### Initial State:

Account: [CREATOR], balance: 0x0, nonce:0, storage:{}
Account: [ATTACKER], balance: 0x0, nonce:0, storage:{}

### Transaction Sequence

Caller: [CREATOR], calldata: , decoded_data: , value: 0x0
Caller: [ATTACKER], function: assertExample(uint256), txdata: 0xeb11813b0000000000000000000000000000000000000000000000000000000000000000, decoded_data: (0,), value: 0x0


