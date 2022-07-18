```
vip: 08
title: Add two proposals to adjust the pledge rate and optimize JsonRpc apis
author: Darylc
status: Final
type: Standards Track
category:  Core & API
created: 2022-03-25
``` 

## Simple Summary

This VIP will add two proposals to adjust the pledge rate and optimize JsonRpc apis

## Abstract

There are two types of the WithdrawBalance transaction, namely SPREAD_MINT and ALL. At present, the withdrawal amount of the transaction info for withdraw transaction does not separate, we need to separate the withdrawal amount, and the spreadMint pledge amount does not participate in the calculation of the entire network pledge rate, it will affect the pledge rate and inflation rate of the entire network and other parameters. 
So we propose to separate the withdrawal amount and allow the SpreadMint participate the calculation of pledge rate parameter.

Then, for failed transactions on the chain, the blockHash, transactionLog, gasUsed, transactionIndex and other fields of the transaction cannot be queried through the eth_getTransactionReceipt method. In the new version, we optimize this method so that you can query more complete information


## Motivation
### Core
The current fixed ALLOW_WITHDRAW_TRANSACTION_INFO_SEPARATE_AMOUNT parameter is 0, instead of being a fixed value, it is better to make the ALLOW_WITHDRAW_TRANSACTION_INFO_SEPARATE_AMOUNT parameter configurable.

The current fixed ALLOW_SPREAD_MINT_PARTICIPATE_PLEDGE_RATE parameter is 0, instead of being a fixed value, it is better to make the ALLOW_SPREAD_MINT_PARTICIPATE_PLEDGE_RATE parameter configurable.

### API
The current result info for failed transactions on the chain, the blockHash, transactionLog, gasUsed, transactionIndex and other fields of the transaction cannot be queried through the eth_getTransactionReceipt method of JsonRpc apis. It will be unsatisfactory for some usage scenarios.

## Specification
The ALLOW_WITHDRAW_TRANSACTION_INFO_SEPARATE_AMOUNT, ALLOW_SPREAD_MINT_PARTICIPATE_PLEDGE_RATE proposal type is defined as :
```
public enum ProposalType {
...
ALLOW_WITHDRAW_TRANSACTION_INFO_SEPARATE_AMOUNT(55),// 0,1
ALLOW_SPREAD_MINT_PARTICIPATE_PLEDGE_RATE(56);// 0,1
...
}
```
The proposal code is 55 and its initial value is set 0. The valid range of ALLOW_WITHDRAW_TRANSACTION_INFO_SEPARATE_AMOUNT parameter is only 1.

The proposal code is 56 and its initial value is set 0. The valid range of ALLOW_SPREAD_MINT_PARTICIPATE_PLEDGE_RATE parameter is 0 or 1.

## Rationale

It is quite necessary to adjust the ALLOW_WITHDRAW_TRANSACTION_INFO_SEPARATE_AMOUNT, ALLOW_SPREAD_MINT_PARTICIPATE_PLEDGE_RATE to adapt to different situations in the VISION network.