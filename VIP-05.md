```
vip: 05
title: JSON RPC
author: Darylc
status: Final
type: Standards Track
category:  API
created: 2022-01-28
``` 

## Simple Summary

This VIP introduces the optimization of JSON-RPC and the statistics of additional assets.

## Abstract

In the current VISION network, the JSON-RPC interface is compatible, but it is not complete for multi-signature and parse-parameters. In this regard, we have optimized signature verification and parameter padding.


## Motivation
For JSON-RPC:
Optimize data parsing format in previous versions and implement some query methods.

For statistics of total additional rewards:
In the current project, there are only total data of additional assets, no additional assets corresponding to each specific resource.



## Rationale

1. Use gasLimit as originEntropyLimit parameter when you deploy the contract using JSON-RPC interface.
2. Transform the precision of the parameter "call_value" to fit the vision network.
3. Add some query methods of JSON-RPC interface.
    ```
      smartBuilder
              .setAbi(abiBuilder)
              .setBytecode(ByteString.copyFrom(this.data))
              .setCallValue(ByteUtil.byteArrayToLongDividePrecision(this.value, "1000000000000")) // transfer to contract
              .setConsumeUserResourcePercent(100)
              .setOriginEntropyLimit(ByteUtil.byteArrayToLong(gasLimit));
      smartBuilder
    ```
4. Add the statistics of total additional rewards of block generation, voting, and spread-mint, where you can get these value from the api "wallet/getnonproposalchainparameters"
   ```
       {
         "key": "getTotalWitnessPayAssets",
         "value": 4719010384
       },
       {
         "key": "getTotalWitness123PayAssets",
         "value": 39325303760
       },
       {
         "key": "getTotalSpreadMintPayAssets",
         "value": 8389369896
       }
   ```