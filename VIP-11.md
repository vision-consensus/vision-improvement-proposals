```
vip: 11
title: Multi-stage freeze and vote weighting
author: Darylc
status: Final
type: Standards Track
category:  CORE
created: 2022-10-17
``` 

## Simple Summary

This VIP introduces the multi-stage resource freezing and the weighting of voting rights and refreeze of the resource.

## Abstract

In the current VISION network, when the user choose to freeze resources to obtain light quantum and entropy, they also obtain voting powers, and they can vote for any first validator to obtain voting benefits. 

In the previous network economic model, the user's voting power will be weighted according to the user's current votes. For example, the weighting coefficient of less than 1000 votes is 1, the weighting coefficient of 1000 to 10000 votes is 1.08, the weighting coefficient of 10000 to 100000 votes is 1.13, and the weighting coefficient of more than 100000 votes The vote weighting factor is 1.16. 

In the new version, we will introduce a new weighted economic model, weighted by freezing time. Vision Network for users (voters) to add according to the freeze stage, vote weighted processing, ALLOW_VP_FREEZE_STAGE_WEIGHT after the opening of proposition 58 to take effect, according to the frozen file, freeze the corresponding period, give the corresponding weight. For example, the stage, the freeze period, the initial configuration of the weight is as follows: 1,35,100; 2,60,110; 3,180,120; 4,360,130; 5,720,150 identification The user's first stage freeze period is 35 days, the weight is 100, the second stage freeze period is 60 days, the weight is 110, the third stage is frozen for 180 days, the weight is 120, the fourth stage is frozen for 360 days, the weight is 130, and the fifth stage is frozen for 720 days and the weight is 150. If the user freezes 1VS, 2VS, 3VS, 4VS, 5VS in five stages, the user voting weight is (1 * 100 + 2 * 110 + 3 * 120 + 4 * 130 + 5 * 150)/ (1 + 2 + 3 + 4 + 5) = 130, so the voting weightvoCountWeight = voteCountWeight 130/100;

## Motivation
For CORE:

Inorder to allow voters to obtain higher voting mining revenue, we have introduced a multi-stage freezing weighting mechanism. This mechanism is more flexible than the previous voting coefficient obtained by freezing photons or entropy.

At the same time, for multi-stage pledges, after the resource freeze time expires, a new reinvestment mechanism is introduced, and during the reinvestment consideration period, the account can choose to unfreeze resources. After entering the reinvestment period, the account can only choose to reinvest Freeze, with the weighting factor continuing to maintain.

## Specification
The ALLOW_VP_FREEZE_STAGE_WEIGHT, VP_FREEZE_STAGE_WEIGHT, REFREEZE_CONSIDERATION_PERIOD, SPREAD_REFREEZE_CONSIDERATION_PERIOD proposal type is defined as :
```
public enum ProposalType {
...
    ALLOW_VP_FREEZE_STAGE_WEIGHT(58), // 0,1
    VP_FREEZE_STAGE_WEIGHT(59), //1,35,100;2,60,110;3,90,120;4,180,130;5,360,150
    REFREEZE_CONSIDERATION_PERIOD(60),//[1,30]
    SPREAD_REFREEZE_CONSIDERATION_PERIOD(61),
...
}
```
The proposal code is 58 and its initial value is set 0. The valid range of ALLOW_VP_FREEZE_STAGE_WEIGHT parameter is [0, 1]. Once turned on, it cannot be turned off.
The proposal code is 59 and its initial value is set ```1,35,100;2,60,110;3,90,120;4,180,130;5,360,150```. The valid parameter is the first stage weight is 100, the last stage weight ie less than 200, and the weighting coefficient increases in order.
The proposal code is 60 and its initial value is set 0. The valid range of REFREEZE_CONSIDERATION_PERIOD parameter is [0, 1]. 
The proposal code is 61 and its initial value is set 0. The valid range of SPREAD_REFREEZE_CONSIDERATION_PERIOD parameter is [0, 1].


## Rationale

1. It is quite necessary to adjust the ALLOW_VP_FREEZE_STAGE_WEIGHT, VP_FREEZE_STAGE_WEIGHT, REFREEZE_CONSIDERATION_PERIOD, SPREAD_REFREEZE_CONSIDERATION_PERIOD to adapt to different situations in the VISION network.
2. We provide five stages options

| stage | duration (day) | weight |
|-------|:---------------|:------:|
| 1     | 35             |  100   |
| 2     | 60             |  110   |
| 3     | 90             |  120   |
| 4     | 180            |  130   |
| 5     | 360            |  150   |

3. The first column of stage represents the stage serial number of multiple stage. The second column of duration represents the freezing time period, the unit is days. The third column of weight represents the weighting coefficients. eg: If you freeze 100vs at stage 2 and freeze 200vs at stage 3, your weighting factor is calculated as:
   weight = (100 * 1.1 + 200 * 1.2) / (100 + 200) = 1.16. 
   
   Then, the weighting factor for the account is 1.16. When the account vote for the first validator's node, the valid voteCountWeight will be multiplied by the weighting factor by the account's current votes, and the weighting factor will also be calculated when calculating the income.
