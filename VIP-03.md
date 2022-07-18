```
vip: 03
title: Vision Economy Model
author: Jerry
status: Final
type: Standards Track
category:  CORE
created: 2020-11-16
``` 

## Simple Summary

This VIP introduces the implementation of Vision Economy Model.

## Abstract

##### Nomenclature

**Economy Cycle**

1. The initial economic cycle is equal to 40 maintenance cycles.
2. The following economic cycle defaults to 120 maintenance cycles.
3. The number of 120 can be updated by proposal ECONOMY_CYCLE

**Pledge Rate**

The frozen amount (VS) related to the whole network voting divided by the whole network liquidity (VS). 

**Inflation Rate**

VS is the primary currency used in the VISION network. The inflation rate of the price of VS within one year. In VISION network, we set the low rate 6.89% and the hight rate 23.22%. We multiply the rate of inflation when we divide the income. For example, really producing block rewards is producing block rewards * (6.89 % / 12 + 1), the same as voting rewards and spread mint rewards.

**Pledge Rate Threshold**

The initial rate threshold is 60%, it can be update by proposal PLEDGE_RATE_THRESHOLD. The Pledge Rate. It will effect the Inflation Rate.

## Motivation

In order to make the blockchain more stable and robust in the economic cycle, flexible conditional yields encourage staking to attract more users to play this ecology

## Rationale

1. Computing the Pledge Rate in every maintenance cycle
2. Computing the average of Pledge Rate when Economy Cycle arrives
3. If the Pledge Rate >= Pledge Rate Threshold , set Inflation Rate is 6.89%
4. If the Pledge Rate < Pledge Rate Threshold , set Inflation Rate is 23.22%
5. Then the reward will multiply the Inflation Rate in next Economy Cycle






