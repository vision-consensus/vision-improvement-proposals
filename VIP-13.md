```
vip: 13
title: Allow setting to modify the community voting node fee
author: Darylc
status: Final
type: Standards Track
category:  CORE
created: 2022-10-19
``` 

## Simple Summary

This VIP introduces a new proposal to allow setting to modify the community voting node fee.

## Abstract

In the current VISION network, the accounts can vote for community nodes to obtain community node mining revenue, and the accounts can also modify their community nodes. 
In the new version, vision network introduces a new proposal, that the first validator create a proposal to control the modification Community node fee.

## Specification
The MODIFY_SPREAD_MINT_PARENT_FEE proposal type is defined as :
```
public enum ProposalType {
...
MODIFY_SPREAD_MINT_PARENT_FEE(63); // [0, 100_000_000L]
...
}
```
The proposal code is 63 and its initial value is set 0. The valid range of MODIFY_SPREAD_MINT_PARENT_FEE parameter is [0, 100,000,000].

## Rationale

1. It is quite necessary to adjust the MODIFY_SPREAD_MINT_PARENT_FEE to adapt to different situations in the VISION network.