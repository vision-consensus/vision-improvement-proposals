```
vip: 09
title: JsonRpc API optimize
author: Lemon
status: Final
type: Standards Track
category:  API
created: 2022-04-13
``` 

## Simple Summary

This VIP introduces the implementation and description of optimizing JsonRpc apis, eth_getLogs, eth_estimateGas and eth_getTransactionByHash

## Abstract

APIs of eth_estimateGas and eth_getTransactionByHash that existed before were imperfect , eth_getLogs did not exist, This VIP will improve the imployments of these JSON-RPC APIs and make them useful

## Motivation
### eth_getLogs

Returns an array of all logs matching a given filter object.

### eth_estimateGas

Generates and returns an estimate of how much gas is necessary to allow the transaction to complete. The transaction will not be added to the blockchain. Note that the estimate may be significantly more than the amount of gas actually used by the transaction, for a variety of reasons including EVM mechanics and node performance.

### eth_getTransactionByHash

Optimizes the result of the information about a transaction requested by transaction hash

## Specification

#### BlockCapsule
```
public class Bloom {

  public static final int BLOOM_BIT_SIZE = 2048;
  public static final int BLOOM_BYTE_SIZE = BLOOM_BIT_SIZE / 8;
  private static final int STEPS_8 = 8;
  private static final int ENSURE_BYTE = 255;
  private static final int LOW_3_BITS = getLowBits(BLOOM_BIT_SIZE);
  private byte[] data = new byte[BLOOM_BYTE_SIZE];
  ...
}
```
#### TransactionExtention
```
message TransactionExtention {
  ...
  int64 entropy_used = 5;
  repeated TransactionInfo.Log logs = 6;
  repeated InternalTransaction internal_transactions = 7;
}
```

#### InternalTransaction
```
message InternalTransaction {
  ...
  string extra = 7;
}
```

## Rationale

In order to be compatible with the Ethereum JSON-RPC and facilitate the access and development of third-party plugin wallets, this is a very necessary function to be implemented, and other interface functions will be gradually supplemented and improved in the future