```
vip: 06
title: Add a proposal to adjust the total photon limit
author: Darylc
status: Final
type: Standards Track
category:  API
created: 2022-02-24
``` 

## Simple Summary

This VIP will add a proposal to adjust the total photon limit.

## Abstract

The total photon limit stands for the photon resource distributed to all the users when they freeze their VS balances. At present, the total photon limit TOTAL_PHOTON_LIMIT parameter is set as a fixed value of 1 billion , which is not flexible enough to adapt to the rapid development of the VISION network. So we propose to change the total photon limit parameter.

## Motivation
The current fixed TOTAL_PHOTON_LIMIT parameter is 1000000000, instead of being a fixed value, it is better to make the TOTAL_PHOTON_LIMIT parameter configurable.

## Specification
The TOTAL_PHOTON_LIMIT proposal type is defined as :
```
public enum ProposalType {
...
TOTAL_PHOTON_LIMIT(51); // 1_000_000_000L, [0, 1000_000_000_000L]
...
}
```
The proposal code is 51 and its initial value is set 1,000,000,000. The valid range of TOTAL_PHOTON_LIMIT parameter is [0, 1000,000,000,000].

## Rationale

It is quite necessary to adjust the total photon limit to adapt to different situations in the VISION network.