```
vip: 12
title: Json-Rpc api compatible with native transactions
author: Darylc
status: Final
type: Standards Track
category:  JSONRPC
created: 2022-10-18
``` 

## Simple Summary

This VIP introduces the evm api compatible vision native transactions.

## Abstract

In the current VISION network, the account cannot apply the first validators, resource freezing, voting for the first validators, withdraw reward and other functions through the JSON-RPC interface.

In the new version, the vision network supports the native transactions of vision can be called through the evm interface. eg: VoteWitnessContract, FreezeBalanceContract, UnfreezeBalanceContract, WithdrawBalanceContract, WitnessCreateContract, WitnessUpdateContract, UpdateBrokerContract, ProposalCreateContract, ProposalApproveContract, ProposalDeleteContract, AccountUpdateContract.

## Motivation
For JSON RPC:

In the previous JSON-RPC interface, only simple transfers, contract calls and basic functions provided by the evm interface were supported, and many transactions that users cared about were missing, resulting in many users unable to call the vision native transactions through the JSON-RPC interface.

## Specification
The ALLOW_ETHEREUM_COMPATIBLE_TRANSACTION_NATIVE_STEP1 proposal type is defined as :
```
public enum ProposalType {
...
    ALLOW_ETHEREUM_COMPATIBLE_TRANSACTION_NATIVE_STEP1(62), // 0,1
...
}
```
The proposal code is 62 and its initial value is set 0. The valid range of ALLOW_ETHEREUM_COMPATIBLE_TRANSACTION_NATIVE_STEP1 parameter is [0, 1].

## Rationale

1. It is quite necessary to adjust the ALLOW_ETHEREUM_COMPATIBLE_TRANSACTION_NATIVE_STEP1 to adapt to different situations in the VISION network.
2. The vision network defines a new standard for evm to support the vision native transaction, that is the vision native transaction type is processed according to the contract method and parameter method specification, the general contract address is ```0x8888888888888888888888888888888888888888```, the transaction type is the contract method, and the transaction parameters are the method parameters of the contract.
3. The following is the abi method of the vision native transaction contract:
   ```
   [
    {
        "stateMutability": "payable",
        "type": "fallback"
    },
    {
        "inputs": [
            {
                "internalType": "string",
                "name": "account_name",
                "type": "string"
            }
        ],
        "name": "accountUpdate",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "string",
                "name": "url",
                "type": "string"
            },
            {
                "internalType": "uint256",
                "name": "upgrade_fee",
                "type": "uint256"
            }
        ],
        "name": "createWitness",
        "outputs": [
            {
                "internalType": "bool",
                "name": "",
                "type": "bool"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "frozen_balance",
                "type": "uint256"
            },
            {
                "internalType": "uint256",
                "name": "frozen_duration",
                "type": "uint256"
            },
            {
                "internalType": "uint256",
                "name": "resource",
                "type": "uint256"
            },
            {
                "internalType": "address",
                "name": "receiver_address",
                "type": "address"
            },
            {
                "internalType": "uint256[]",
                "name": "stages",
                "type": "uint256[]"
            },
            {
                "internalType": "uint256[]",
                "name": "frozen_balances",
                "type": "uint256[]"
            }
        ],
        "name": "freezeBalance",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "payable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "frozen_balance",
                "type": "uint256"
            },
            {
                "internalType": "uint256",
                "name": "frozen_duration",
                "type": "uint256"
            },
            {
                "internalType": "uint256",
                "name": "resource",
                "type": "uint256"
            },
            {
                "internalType": "address",
                "name": "receiver_address",
                "type": "address"
            },
            {
                "internalType": "uint256[]",
                "name": "stages",
                "type": "uint256[]"
            },
            {
                "internalType": "uint256[]",
                "name": "frozen_balances",
                "type": "uint256[]"
            },
            {
                "internalType": "bool[]",
                "name": "refreezes",
                "type": "bool[]"
            }
        ],
        "name": "freezeBalance",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "payable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "frozen_balance",
                "type": "uint256"
            },
            {
                "internalType": "uint256",
                "name": "frozen_duration",
                "type": "uint256"
            },
            {
                "internalType": "uint256",
                "name": "resource",
                "type": "uint256"
            },
            {
                "internalType": "address",
                "name": "receiver_address",
                "type": "address"
            }
        ],
        "name": "freezeBalance",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "payable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "address",
                "name": "owner_address",
                "type": "address"
            }
        ],
        "name": "getBrokerage",
        "outputs": [
            {
                "internalType": "uint256",
                "name": "brokerage",
                "type": "uint256"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [],
        "name": "getNextMaintenanceTime",
        "outputs": [
            {
                "internalType": "uint256",
                "name": "num",
                "type": "uint256"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "address",
                "name": "owner_address",
                "type": "address"
            }
        ],
        "name": "getReward",
        "outputs": [
            {
                "internalType": "uint256",
                "name": "reward",
                "type": "uint256"
            },
            {
                "internalType": "uint256",
                "name": "spreadReward",
                "type": "uint256"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "proposal_id",
                "type": "uint256"
            },
            {
                "internalType": "bool",
                "name": "is_add_approval",
                "type": "bool"
            }
        ],
        "name": "proposalApprove",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "proposal_id",
                "type": "uint256"
            },
            {
                "internalType": "string",
                "name": "proposal_value",
                "type": "string"
            }
        ],
        "name": "proposalCreate",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "proposal_id",
                "type": "uint256"
            },
            {
                "internalType": "uint256",
                "name": "proposal_value",
                "type": "uint256"
            }
        ],
        "name": "proposalCreateUint",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "proposal_id",
                "type": "uint256"
            }
        ],
        "name": "proposalDelete",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "resource",
                "type": "uint256"
            },
            {
                "internalType": "address",
                "name": "receiver_address",
                "type": "address"
            }
        ],
        "name": "unfreezeBalance",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "resource",
                "type": "uint256"
            },
            {
                "internalType": "address",
                "name": "receiver_address",
                "type": "address"
            },
            {
                "internalType": "uint256[]",
                "name": "stages",
                "type": "uint256[]"
            }
        ],
        "name": "unfreezeBalance",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "brokerage",
                "type": "uint256"
            }
        ],
        "name": "updateBrokerage",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "string",
                "name": "update_url",
                "type": "string"
            }
        ],
        "name": "updateWitness",
        "outputs": [
            {
                "internalType": "bool",
                "name": "",
                "type": "bool"
            }
        ],
        "stateMutability": "payable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "address[]",
                "name": "vote_address",
                "type": "address[]"
            },
            {
                "internalType": "uint256[]",
                "name": "vote_count",
                "type": "uint256[]"
            }
        ],
        "name": "voteWitness",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "withdraw_type",
                "type": "uint256"
            }
        ],
        "name": "withdrawBalance",
        "outputs": [
            {
                "internalType": "bytes32",
                "name": "hash",
                "type": "bytes32"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "stateMutability": "payable",
        "type": "receive"
    }
   ]
   
   ```