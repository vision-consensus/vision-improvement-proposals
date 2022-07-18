```
vip: 04
title: Sort Witness not by block
author: Derrick
status: Final
type: Standards Track
category:  CORE
created: 2020-12-16
``` 

## Simple Summary

This VIP introduces the implementation of Sort Witness not by block.

## Simple Summary

We sort the witnesses according to their total votes, which is the most important functional indicator to highlight the witnesses.

## Abstract

We use the total number of votes of the witness itself and the sum of the votes of all other voters on the vision for the witness to rank the witness, and use this result as the block sequence for the next maintenance cycle.

## Motivation

Witness is the most influential representative in the entire chain. Under this premise, we need to quantify the function of witness, and voting is the best embodiment.
## Rationale

#### sortWitness

```
  private void sortWitness(List<ByteString> list) {
    list.sort(Comparator.comparingLong((ByteString b) -> {
      WitnessCapsule witnessCapsule = getWitnessByAddress(b);
      return Math.min(witnessCapsule.getVoteCountWeight(), witnessCapsule.getVoteCountThreshold());
    }).thenComparing((ByteString b) ->
            getWitnessByAddress(b).getVoteCountWeight())
        .reversed().thenComparing(Comparator.comparingInt(ByteString::hashCode).reversed()));
  }
```