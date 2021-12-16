```
vip: 01
title: SPREAD MINT
author: Darylc
status: Final
type: Standards Track
category:  CORE
created: 2020-11-12
``` 

## Simple Summary

This VIP introduces the implementation and description of SpreaMint, and the calculation method of reward who participating in SpreadMint 

## Abstract

Users freeze VS to get Spread Mint rewards. When freezing, they must fill in the parent account address, and the settlement will be settled according to the proportion. Vision initially defaults to a three-level promotion model, and the coefficient ratios for sharing rewards are 80%, 10%, 8%, and 2% respectively.

**Scenario 1**: 

Linked Model:
Alice(A) is participating in SpreadMint and needs to fill in the upper-level account address Bob(B) and freeze balances 100VS.
Bob(B) is participating in SpreadMint and needs to fill in the upper-level account address Carl(C) and freeze balances 80VS.
Carl(C) is participating in SpreadMint and needs to fill in the upper-level account address Dary(D) and freezes balances 10VS.
Dary(D) is not participating in SpreadMint or freezing balance is 0VS.
Then the parent relationship link is like: A->B->C->D, and the ratio will be calculated when the settlement are A get 80% * rewards, B get 10% * rewards * 80 / 100, C get 8% * rewards * 10 / 80, D get 2% * rewards * 0 / 10

**Scenario 2**: 

Cycle Model:
Alice(A) is participating in SpreadMint and needs to fill in the upper-level account address Bob(B) and freeze balances 100VS.
Bob(B) is participating in SpreadMint and needs to fill in the upper-level account address Carl(C) and freeze balances 80VS.
Carl(C) is participating in SpreadMint and needs to fill in the upper-level account address Alice(A) and freezes balances 10VS.

Then the parent relationship link is like: A->B->C->A, and the ratio will be calculated when the settlement are A get 80% * rewards, B get 10% * rewards * 80 / 100, C get 8% * rewards * 10 / 80, A get none rewards.


## Motivation

SpreadMint is one of three rewards. Both First Validators and ordinary users can get extra rewards by participating in SpearMint, just fill in the upper-level address and free some balances.


## Rationale

The First Validator generates a Spreadmint reward every time a block is produced, and users can participate by freezing Spread.
At the end of the maintenance period, the income during the maintenance period will be counted and recorded on the chain.
When the user settles, according to the maintenance period of the last withdrawal of SpreadMint to the current maintenance period, all rewards

#### Account

```
message Account {
  ...
  int64 balance = 4;
  ...
  repeated Frozen frozen = 7;
  int64 allowance = 0x0B;
  ...
  message AccountResource {
    // the frozen balance for spread_mint
    Frozen frozen_balance_for_spread = 9;
  }
  ...
  int64 spread_mint_allowance = 34;
}
```

#### reward
```
message RewardMessage {
  int64 reward = 1;
  int64 spreadReward = 2;
}
```
