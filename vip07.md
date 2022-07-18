```
vip: 07
title: Add three proposals to adjust the pledge period or clear vote
author: Darylc
status: Final
type: Standards Track
category:  Core
created: 2022-03-14
``` 

## Simple Summary

This VIP will add three proposals to adjust the pledge period and whether to unfreeze clear votes

## Abstract

At present, the freeze period for obtaining photons or entropy and voting rights through pledge VS is 3 days, and the freeze period for the first validator to stake VS in order to obtain the vote weight is 23 days, which is not flexible enough to adapt to the rapid development of the VISION network. So we propose to change the special freeze period limit and the fvguarantee freeze period limit parameter.
Then, unfreeze the SpreadMint and FVGURARANTEE will clear the votes that have been cast. If they want to continue to vote for the node after unfreezing, they need to vote again. So we propose to change the ALLOW_UNFREEZE_SPREAD_OR_FVGUARANTEE_CLEAR_VOTE parameter.


## Motivation
The current fixed SPECIAL_FREEZE_PERIOD_LIMIT parameter is 3, instead of being a fixed value, it is better to make the SPECIAL_FREEZE_PERIOD_LIMIT parameter configurable.
The current fixed FVGUARANTEE_FREEZE_PERIOD_LIMIT parameter is 23, instead of being a fixed value, it is better to make the FVGUARANTEE_FREEZE_PERIOD_LIMIT parameter configurable.
The current fixed ALLOW_UNFREEZE_SPREAD_OR_FVGUARANTEE_CLEAR_VOTE parameter is 1, instead of being a fixed value, it is better to make the FVGUARANTEE_FREEZE_PERIOD_LIMIT parameter configurable. It means that unfreeze the Spreadmint pledge and FVGURARANTEE pledge will clear the votes that have been cast. If they want to continue to vote for the node after unfreezing, they need to vote again. 

## Specification
The SPECIAL_FREEZE_PERIOD_LIMIT, FVGUARANTEE_FREEZE_PERIOD_LIMIT,ALLOW_UNFREEZE_SPREAD_OR_FVGUARANTEE_CLEAR_VOTE proposal type is defined as :
```
public enum ProposalType {
...
SPECIAL_FREEZE_PERIOD_LIMIT(52),// [1, 365L]
FVGUARANTEE_FREEZE_PERIOD_LIMIT(53),// [1, 365L]
ALLOW_UNFREEZE_SPREAD_OR_FVGUARANTEE_CLEAR_VOTE(54);// 0,1
...
}
```
The proposal code is 52 and its initial value is set 3. The valid range of SPECIAL_FREEZE_PERIOD_LIMIT parameter is [1, 365].
The proposal code is 53 and its initial value is set 23. The valid range of FVGUARANTEE_FREEZE_PERIOD_LIMIT parameter is [1, 365].
The proposal code is 54 and its initial value is set 1. The valid range of ALLOW_UNFREEZE_SPREAD_OR_FVGUARANTEE_CLEAR_VOTE parameter is {0, 1}.

## Rationale

It is quite necessary to adjust the SPECIAL_FREEZE_PERIOD_LIMIT, FVGUARANTEE_FREEZE_PERIOD_LIMIT, ALLOW_UNFREEZE_SPREAD_OR_FVGUARANTEE_CLEAR_VOTE to adapt to different situations in the VISION network.