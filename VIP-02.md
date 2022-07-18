```
vip: 02
title: Ethereum Transaction Compatible
author: Darylc
status: Final
type: Standards Track
category:  CORE
created: 2020-11-15
```

## Simple Summary

This VIP introduces that How VISION realizes Ethereum Transaction Compatible. A json-rpc server to support Eth's Transaction like [Eth's json-rpc API](https://eth.wiki/json-rpc/API).

## Abstract

VISION's Ethereum Transaction Compatible was created to meet the needs of secure and usable Ethereum-based web sites. 

## Motivation

Users can request accounts, read data from blockchains the user is connected to, and suggest that the user sign messages and transactions. 

Three important operations, query balances of the account, transfer ordinary tokens VS, deploy the VRC20 smart contract, and trigger the VRC20 smart contract to send tokens.


## Rationale

#### json-rpc server

```
    ...
    String eth_chainId();
    String web3_clientVersion();
    String web3_sha3(String data) throws Exception;
    String net_version();
    String net_peerCount();
    boolean net_listening();
    String eth_protocolVersion();
    Object eth_syncing();
    String eth_coinbase();
    boolean eth_mining();
    String eth_hashrate();
    String eth_gasPrice();
    String[] eth_accounts();
    String eth_blockNumber();
    String eth_getBalance(String address, String block) throws Exception;
    String eth_getLastBalance(String address) throws Exception;
    String eth_getStorageAt(String address, String storageIdx, String blockId) throws Exception;
    String eth_getTransactionCount(String address, String blockId) throws Exception;
    String eth_getBlockTransactionCountByHash(String blockHash)throws Exception;
    String eth_getBlockTransactionCountByNumber(String bnOrId)throws Exception;
    String eth_getUncleCountByBlockHash(String blockHash)throws Exception;
    String eth_getUncleCountByBlockNumber(String bnOrId)throws Exception;
    String eth_getCode(String addr, String bnOrId)throws Exception;
    String eth_sign(String addr, String data) throws Exception;
    String eth_sendTransaction(CallArguments transactionArgs) throws Exception;
    String eth_sendRawTransaction(String rawData) throws Exception;
    String eth_call(CallArguments args, String bnOrId) throws Exception;
    String eth_estimateGas(CallArguments args) throws Exception;
    BlockResult eth_getBlockByHash(String blockHash, Boolean fullTransactionObjects) throws Exception;
    BlockResult eth_getBlockByNumber(String bnOrId, Boolean fullTransactionObjects) throws Exception;
```

#### RLP data

```
    public synchronized void rlpParse() {
      if (parsed) return;
      try {
        RLPList decodedTxList = RLP.decode2(rlpEncoded);
        RLPList transaction = (RLPList) decodedTxList.get(0);

        // Basic verification
        if (transaction.size() > 9 ) throw new RuntimeException("Too many RLP elements");
        for (RLPElement rlpElement : transaction) {
          if (!(rlpElement instanceof RLPItem))
            throw new RuntimeException("Transaction RLP elements shouldn't be lists");
        }

        this.nonce = transaction.get(0).getRLPData();
        this.gasPrice = transaction.get(1).getRLPData();
        this.gasLimit = transaction.get(2).getRLPData();
        this.receiveAddress = transaction.get(3).getRLPData();
        this.value = transaction.get(4).getRLPData();
        this.data = transaction.get(5).getRLPData();
        // only parse signature in case tx is signed
        if (transaction.get(6).getRLPData() != null) {
          byte[] vData =  transaction.get(6).getRLPData();
          BigInteger v = ByteUtil.bytesToBigInteger(vData);
          byte[] r = transaction.get(7).getRLPData();
          byte[] s = transaction.get(8).getRLPData();
          this.chainId = extractChainIdFromRawSignature(v, r, s);
          if (r != null && s != null) {
            this.signature = ECDSASignature.fromComponents(r, s, getRealV(v));
          }
        } else {
          logger.debug("RLP encoded tx is not signed!");
        }
        this.hash = Hash.sha3(rlpEncoded);
        this.parsed = true;
      } catch (Exception e) {
        throw new RuntimeException("Error on parsing RLP", e);
      }
    }
```

**Send VS**: 

```
message TransferContract {
  bytes owner_address = 1;
  bytes to_address = 2;
  int64 amount = 3;
  int64 type = 4;  //if type=eth validate eth sign else validate vision sign  0 or null -> vision, 1 -> eth
  bytes rlp_data = 5; // eth's RLP rawData
}
```

**Create VRC20 Contract**: 

```
message CreateSmartContract {
  bytes owner_address = 1;
  SmartContract new_contract = 2;
  int64 call_token_value = 3;
  int64 token_id = 4;
  int64 type = 5; //if type=eth validate eth sign else validate vision sign  0 or null -> vision, 1 -> eth
  bytes rlp_data = 6; // eth's RLP rawData
}
```

**Send VRC20**: 

```
message TriggerSmartContract {
  bytes owner_address = 1;
  bytes contract_address = 2;
  int64 call_value = 3;
  bytes data = 4;
  int64 call_token_value = 5;
  int64 token_id = 6;
  int64 type = 7; //if type=eth validate eth sign else validate vision sign  0 or null -> vision, 1 -> eth
  bytes rlp_data = 8; // eth's RLP rawData
}
```



