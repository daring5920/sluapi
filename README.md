## "# silubium API"  ##

SLU公用接口程序，为手机钱包、网页钱包等应用提供接口调用。
网址：http://47.107.38.202:6910 

### 具体调用方法： ###

## Tokens
* [ALL Tokens](#all-tokens)
* [Token Account Balance](#token-account-balance)
* [Token Total supply](#token-total-supply)
* [Token Transactions](#token-transactions)
* [Token Transfer](#token-transfer)

## Table of Contents
* [Account Info](#account-info)
* [SRC20 info](#src20-info)
* [SRC20 transfers](#src20-transfers)
* [SRC20 balances](#src20-balances)

### Statistics
* [Total 24h](#total-24h-statistic)
* [Transactions](#transactions-statistic)
* [Fees](#fees-statistic)
* [Outputs](#outputs-statistic)
* [Difficulty](#difficulty-statistic)
* [Stake](#stake-statistic)
* [Total Supply](#total-supply-statistic)

### Block Transaction
* [Block Hash](#block-hash)
* [Block Index](#block-index)
* [Raw Block](#raw-block)
* [Block Summaries](#block-summaries)
* [Transaction](#transaction)
* [Address](#address)
* [Address Properties](#address-properties)
* [Unspent Outputs](#unspent-outputs)
* [Unspent Outputs for Multiple Addresses](#unspent-outputs-for-multiple-addresses)
* [Transactions by Block](#transactions-by-block)
* [Transactions by Address](#transactions-by-address)
* [Transactions Receipt](#transactions-receipt)
* [Transactions for Multiple Addresses](#transactions-for-Multiple-Addresses)
* [Transaction Broadcasting](#Transaction-Broadcasting)
* [Historic Blockchain Data Sync Status](#Historic-Blockchain-Data-Sync-Status)
* [Live Network P2P Data Sync Status](#Live-Network-P2P-Data-Sync-Status)
* [Status of the SILUBIUM Network](#Status-of-the-SILUBIUM-Network)
* [Estimatefee](#Utility-Methods)
* [Minestimatefee](#Min-Estimate-Fee-Per-KB)



---
凡是返回多条数据的分页参数均为

            `limit=<Number>`
            
                > MAX_LIMIT === 100
            
            `offset=<Number>`
---

## Tokens

### ALL Tokens

```
  `GET` /silubium-api/tokens
```

* **SLUuery Params**
  
    * **Optional:**
        
            `limit=<Number>`
            
                > MAX_LIMIT === 100
            
            `offset=<Number>`
            
            `order=time`
没有order参数是默认按照持有人数量倒序，有order且值为time是按照时间倒序           
This would return:

```
{
limit: 100,
offset: 0,
count: 19,
items: [
          {
          count_holders: 6,
          tx_hash: "4f349f09851c6e54291d468e95c9a182c30729b0d115810dfadacc8501efb6af",
          vout_idx: 0,
          updated_at: "2018-08-13T01:27:05.546Z",
          block_height: 11682,
          contract_address: "0973e4b1598b5badf72076cb08727936f41ab40a",
          contract_address_base: "SLUN9ywygdWW1pcVTtSHnsXTomehRhnduqL9",
          decimals: "8",
          name: "WLToken",
          symbol: "WLT",
          total_supply: "1000000000000000000",
          version: "",
          exception: false,
          created_at: "2018-08-13T01:27:05.546Z",
          description: null,
          tx_date_time: "2018-08-05T03:02:40.000Z",
          tx_time: 1533438160
          }
      ]
}
```

### Token Account Balance

```
  `GET` /silubium-api/tokens/{:tokenAddressBase}/addresses/{:addressBase}/balance
```
or
```
  `GET` /silubium-api/tokens/{:tokenAddressBase}/addresses/{:addressBase}/balance?format=object
```

* **SLUquery Params**

    * **Optional:**
        
            `format=object`
            
This would return:

```
1000000000000000000
```

```
{
    "balance": "1000000000000000000"
}
```



### Token Total supply
```
    `GET` /silubium-api/tokens/{:tokenAddressBase}/total-supply
```
or
```
  `GET` /silubium-api/tokens/{:tokenAddressBase}/total-supply?format=object
```

* **SLUquery Params**

    * **Optional:**
        
            `format=object`
            
This would return:

```
"1000000000000000000"
```
or
```
{
    "total_supply": "1000000000000000000"
}
```

### Token Transactions

```
  `GET` /silubium-api/tokens/{:tokenAddressBase}/transactions
```

* **SLUquery Params**

    * **Optional:**
        
            `limit=<Number>`
            
                > MAX_LIMIT === 100
            
            `offset=<Number>`
            
            `from_block=<Number>`
            
            `to_block=<Number>`
            
            `from_date_time=<ISO8601 Date>`
            
            `to_date_time=<ISO8601 Date>`
            
            `addresses=<Array.<String>>`


E.g.:
```
  `GET` /silubium-api/tokens/SLUNdW79juyJNJ89h99D9vfo5SLUhCZpmavJNX/transactions?limit=20&offset=1&from_block=34101&to_block=34378&from_date_time=2017-10-27T01:23:10.000Z&to_date_time=2018-10-27T01:24:10.000Z&addresses[]=SLUbmrFnBhyMKUhrabXfaAWZTncSWbJA8FsG&addresses[]=SLUarHW2HjV8Z3njxiTuvUZU3hmqahKNZ49y
```

This would return:
```
{
    "limit": 20,
    "offset": 1,
    "addresses": [
        "SLUbmrFnBhyMKUhrabXfaAWZTncSWbJA8FsG",
        "SLUarHW2HjV8Z3njxiTuvUZU3hmqahKNZ49y"
    ],
    "from_block": 34101,
    "to_block": 34378,
    "from_date_time": "2017-10-27T01:23:10.000Z",
    "to_date_time": "2018-10-27T01:24:10.000Z",
    "count": 2,
    "items": [
        {
            "contract_address_base": "SLUNdW79juyJNJ89h99D9vfo5SLUhCZpmavJNX",
            "block_height": 34377,
            "tx_hash": "e5c16ea5785fed909957100c3721a62f5f5dfe427af1c926ba11e64c3f905fab",
            "from": "SLUNvEBPtXwezdJjkUUy2JF6pirGn1vtkaNt",
            "to": "SLUarHW2HjV8Z3njxiTuvUZU3hmqahKNZ49y",
            "value": "100000000000",
            "block_date_time": "2017-10-27T12:28:48.000Z"
        }
    ]
}
```

### Token Transfer

```
  `GET` /silubium-api/tokenTransfer
```

* **SLUquery Params**

    * **Optional:**
        
            `limit=<Number>`
            
                > MAX_LIMIT === 100
            
            `offset=<Number>`
            
            `address=<Array.<String>>`

            `contractAddress=<String>`
            
            `txHash=<String>`


E.g.:
```
  `GET` /silubium-api/tokenTransfer?limit=20&offset=1&contractAddress=894ef9231afccd6a8990065fe63a5d10c1b9477e&address[]=SLUZt8DT8u2JTyA8y37kKLWW79UfTFj7NXFS&address[]=SLUZt8DT8u2JTSD8y37kKLWW79UfTFj7NXFS
```

This would return:
```
{
limit: 100,
offset: 0,
count: 5,
items: [
          {
          contract_address: "894ef9231afccd6a8990065fe63a5d10c1b9477e",
          tx_hash: "b742370ad99f00c166938ae25bf47f24455f54cb56a9e34ca0b8a19ac71e20d7",
          tx_time: 1533883536,
          from: "SLUa1q4eirBGuhqguea6d1KKvLeeStMZL7d7",
          from_eth: "8b8aa883da15e5214db0ab48608eb91a5ed18ab5",
          to: "SLUgBcEb7YcjGqCvuyD6FCFkh1wL42v3Whto",
          to_eth: "cf34dd1f3248a639761b9b03ccbed8fb6209d90e",
          value: "5000000000",
          decimals: "8",
          symbol: "EES"
          }
    ]
}
```

## API HTTP Endpoints

### Account Info
```
  `GET` /silubium-api/contracts/{:contractHash}/info
```
This would return:
```
{
    address: "f8fe26582d6ce7f0233aee0477de5be606cca653",
    balance: 0,
    storage: {
            03: "6f",
            00: "5374616e64617264000000000000000000000000000000000000000000000010",
            02: "5354440000000000000000000000000000000000000000000000000000000006",
            03c2cc9c95da7ca004141242c8b36d98e928596f771044fd5552d3ee8b47438f: "2710",
            04: "2710",
            01: "5374616e64617264200000000000000000000000000000000000000000000012"
        },
    code: "606060405236156100b8576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806306fdde03146100ce578063095ea7b31461016757806318160ddd146101be57806323b872dd146101e4578063313ce5671461025a5780633867ed23146102865780635a3b7e421461029857806370a082311461033157806395d89b411461037b578063a9059cbb14610414578063cae9ca5114610453578063dd62ed3e146104ed575b34156100c057fe5b6100cc5b60006000fd5b565b005b34156100d657fe5b6100de610556565b604051808060200182810382528381815181526020019150805190602001908083836000831461012d575b80518252602083111561012d57602082019150602081019050602083039250610109565b505050905090810190601f1680156101595780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b341561016f57fe5b6101a4600480803573ffffffffffffffffffffffffffffffffffffffff169060200190919080359060200190919050506105f4565b604051808215151515815260200191505060405180910390f35b34156101c657fe5b6101ce610682565b6040518082815260200191505060405180910390f35b34156101ec57fe5b610240600480803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803573ffffffffffffffffffffffffffffffffffffffff16906020019091908035906020019091905050610688565b604051808215151515815260200191505060405180910390f35b341561026257fe5b61026a610984565b604051808260ff1660ff16815260200191505060405180910390f35b341561028e57fe5b610296610997565b005b34156102a057fe5b6102a86109ab565b60405180806020018281038252838181518152602001915080519060200190808383600083146102f7575b8051825260208311156102f7576020820191506020810190506020830392506102d3565b505050905090810190601f1680156103235780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b341561033957fe5b610365600480803573ffffffffffffffffffffffffffffffffffffffff16906020019091905050610a49565b6040518082815260200191505060405180910390f35b341561038357fe5b61038b610a61565b60405180806020018281038252838181518152602001915080519060200190808383600083146103da575b8051825260208311156103da576020820191506020810190506020830392506103b6565b505050905090810190601f1680156104065780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b341561041c57fe5b610451600480803573ffffffffffffffffffffffffffffffffffffffff16906020019091908035906020019091905050610aff565b005b341561045b57fe5b6104d3600480803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803590602001909190803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091905050610cde565b604051808215151515815260200191505060405180910390f35b34156104f557fe5b610540600480803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803573ffffffffffffffffffffffffffffffffffffffff16906020019091905050610e65565b6040518082815260200191505060405180910390f35b60018054600181600116156101000203166002900480601f0160208091040260200160405190810160405280929190818152602001828054600181600116156101000203166002900480156105ec5780601f106105c1576101008083540402835291602001916105ec565b820191906000526020600020905b8154815290600101906020018083116105cf57829003601f168201915b505050505081565b600081600660003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550600190505b92915050565b60045481565b600081600560008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205410156106d75760006000fd5b600560008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205482600560008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020540110156107655760006000fd5b600660008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020548211156107ef5760006000fd5b81600560008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000206000828254039250508190555081600560008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000206000828254019250508190555081600660008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600082825403925050819055508273ffffffffffffffffffffffffffffffffffffffff168473ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef846040518082815260200191505060405180910390a3600190505b9392505050565b600360009054906101000a900460ff1681565b60646004600082825401925050819055505b565b60008054600181600116156101000203166002900480601f016020809104026020016040519081016040528092919081815260200182805460018160011615610100020316600290048015610a415780601f10610a1657610100808354040283529160200191610a41565b820191906000526020600020905b815481529060010190602001808311610a2457829003601f168201915b505050505081565b60056020528060005260406000206000915090505481565b60028054600181600116156101000203166002900480601f016020809104026020016040519081016040528092919081815260200182805460018160011615610100020316600290048015610af75780601f10610acc57610100808354040283529160200191610af7565b820191906000526020600020905b815481529060010190602001808311610ada57829003601f168201915b505050505081565b80600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020541015610b4c5760006000fd5b600560008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205481600560008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054011015610bda5760006000fd5b80600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000206000828254039250508190555080600560008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600082825401925050819055508173ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040518082815260200191505060405180910390a35b5050565b60006000849050610cef85856105f4565b15610e5c578073ffffffffffffffffffffffffffffffffffffffff16638f4ffcb1338630876040518563ffffffff167c0100000000000000000000000000000000000000000000000000000000028152600401808573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020018481526020018373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200180602001828103825283818151815260200191508051906020019080838360008314610df8575b805182526020831115610df857602082019150602081019050602083039250610dd4565b505050905090810190601f168015610e245780820380516001836020036101000a031916815260200191505b5095505050505050600060405180830381600087803b1515610e4257fe5b6102c65a03f11515610e5057fe5b50505060019150610e5d565b5b509392505050565b60066020528160005260406000206020528060005260406000206000915091505054815600a165627a7a72305820ad65da1f64921dfd4eebad40d0b4c8f4a800ccd86080446b7ea98cbc56f244f80029",
    vins: [
        {
            hash: "2c329c6793f21b1655be8940bf46b0fae6af303e142b39d1c813796970321124",
            vout: 0,
            amount: 0
        }
    ]
}
```

## Statistics

### Total 24h Statistic
```
  `GET` /silubium-api/statistics/total
```
This would return:
```
    {
        n_blocks_mined: 1268,
        time_between_blocks: 86301,
        mined_currency_amount: 1268000000000000,
        transaction_fees: 633992859997,
        number_of_transactions: 2547,
        outputs_volume: 46920965480,
        difficulty: 981808167.7687966,
        stake: 0.17279912782774598
    }
```
### Transactions Statistic
```
  `GET` /silubium-api/statistics/transactions?days=14
```
This would return:
```
[
    {
        date: "2017-05-30",
        transaction_count: 1087,
        block_count: 541
    },
    ...
]
```

### Fees Statistic
```
  `GET` /silubium-api/statistics/fees?days=14
```
This would return:
```
[
   {
       date: "2017-06-06",
       fee: 500000000
   },
   ...
]
```
### Outputs Statistic
```
  `GET` /silubium-api/statistics/outputs?days=14
```
This would return:
```
[
   {
       date: "2017-06-06",
       sum: 0
   },
   ...
]
```
### Difficulty Statistic
```
  `GET` /silubium-api/statistics/difficulty?days=14
```
This would return:
```
[
    {
        date: "2017-06-06",
        sum: 0
    },
    ...
]
```
### Stake Statistic
```
  `GET` /silubium-api/statistics/stake?days=14
```
This would return:
```
[
    {
        date: "2017-06-06",
        sum: 0
    },
    ...
]
```

### Total Supply Statistic

```
  `GET` /silubium-api/statistics/circulating-supply
```
or
```
  `GET` /silubium-api/statistics/circulating-supply/?format=object
```
This would return:
```
88410384
```
or
```
{
"circulatingSupply": "88410384"
}
```


```
  `GET` /silubium-api/statistics/supply
```
or
```
  `GET` /silubium-api/statistics/supply?format=object
```
This would return:
```
100091264
```
or
```
{
    "supply": "100091264"
}
```
## Block

### Block Hash
```
  /silubium-api/block/[:hash]
  /silubium-api/block/00000000a967199a2fad0877433c93df785a8d8ce062e5f9b451cd1397bdbf62
```
This would return:
```
{
    hash: "9f4157e6359e614b35b764606ae5ca9c48d9e6b1456a4e6950a5d58b46ecd764",
    size: 756,
    height: 24707,
    version: 536870912,
    merkleroot: "aa122c20ef9dff69124a544358faf9dd5d47837588fe787a8a57c098dc7760c7",
    tx: [
    "b9fd02c5a457350d377d764d5ccb4481298683d5f26d99847e7d5668ea92a125",
    "e9aa8c6731df2b739c5fc269735cd7a066e2d684dcdae02a2a14e9bca91fe3e5"
    ],
    time: 1535333040,
    nonce: 0,
    bits: "1a01d845",
    difficulty: 9094174.99077757,
    chainwork: "000000000000000000000000000000000000000000000027b46396404b6989fa",
    confirmations: 1,
    previousblockhash: "d122f8479a37b993405aafbf7bb4d9672a5d0b7302e8ba538a80e758b563a879",
    flags: "proof-of-stake",
    reward: 1,
    isMainChain: true,
    minedBy: "SLUfuqUBeWQeVgjknL68xe8jx3oKK8LEucYQ",
    poolInfo: { }
}
```

### Block Index
Get block hash by height
```
  /silubium-api/block-index/[:height]
  /silubium-api/block-index/0
```
This would return:
```
{
  "blockHash":"000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f"
}
```
which is the hash of the Genesis block (0 height)


### Raw Block
```
  /silubium-api/rawblock/[:blockHash]
  /silubium-api/rawblock/[:blockHeight]
```

This would return:
```
{
  "rawblock":"blockhexstring..."
}
```

### Block Summaries

Get block summaries by date:
```
  /silubium-api/blocks?limit=3&blockDate=2016-04-22
```

Example response:
```
{
  "blocks": [
    {
      "height": 408495,
      "size": 989237,
      "hash": "00000000000000000108a1f4d4db839702d72f16561b1154600a26c453ecb378",
      "time": 1461360083,
      "txlength": 1695,
      "poolInfo": {
        "poolName": "BTCC Pool",
        "url": "https://pool.btcc.com/"
      }
    }
  ],
  "length": 1,
  "pagination": {
    "next": "2016-04-23",
    "prev": "2016-04-21",
    "currentTs": 1461369599,
    "current": "2016-04-22",
    "isToday": true,
    "more": true,
    "moreTs": 1461369600
  }
}
```

### Transaction
```
  /silubium-api/tx/[:txid]
  /silubium-api/tx/525de308971eabd941b139f46c7198b5af9479325c2395db7f2fb5ae8562556c
  /silubium-api/rawtx/[:rawid]
  /silubium-api/rawtx/525de308971eabd941b139f46c7198b5af9479325c2395db7f2fb5ae8562556c
```

### Address
```
  /silubium-api/addr/[:addr][?noTxList=1][&from=&to=]
  /silubium-api/addr/mmvP3mTe53qxHdPqXEvdu8WdC7GfSLU2vmx5?noTxList=1
  /silubium-api/addr/mmvP3mTe53qxHdPqXEvdu8WdC7GfSLU2vmx5?from=1000&to=2000
```

### Address Properties
```
  /silubium-api/addr/[:addr]/balance
  /silubium-api/addr/[:addr]/totalReceived
  /silubium-api/addr/[:addr]/totalSent
  /silubium-api/addr/[:addr]/unconfirmedBalance
```
The response contains the value in Satoshis.

### Unspent Outputs
```
  /silubium-api/addr/[:addr]/utxo
```
Sample return:
```
[
  {
    "address":"mo9ncXisMeAoXwqcV5EWuyncbmCcSLUN4rVs",
    "txid":"d5f8a96faccf79d4c087fa217627bb1120e83f8ea1a7d84b1de4277ead9bbac1",
    "vout":0,
    "scriptPubKey":"76a91453c0307d6851aa0ce7825ba883c6bd9ad242b48688ac",
    "amount":0.000006,
    "satoshis":600,
    "confirmations":0,
    "ts":1461349425
  },
  {
    "address": "mo9ncXisMeAoXwqcV5EWuyncbmCcSLUN4rVs",
    "txid": "bc9df3b92120feaee4edc80963d8ed59d6a78ea0defef3ec3cb374f2015bfc6e",
    "vout": 1,
    "scriptPubKey": "76a91453c0307d6851aa0ce7825ba883c6bd9ad242b48688ac",
    "amount": 0.12345678,
    "satoshis: 12345678,
    "confirmations": 1,
    "height": 300001
  }
]
```

### Unspent Outputs for Multiple Addresses
GET method:
```
  /silubium-api/addrs/[:addrs]/utxo
  /silubium-api/addrs/2NF2baYuJAkCKo5onjUKEPdARSLUkZ6SYyKd5,2NAre8sX2povnjy4aeiHKeEh97SLUhn97tB1f/utxo
```

POST method:
```
  /silubium-api/addrs/utxo
```

POST params:
```
addrs: 2NF2baYuJAkCKo5onjUKEPdARSLUkZ6SYyKd5,2NAre8sX2povnjy4aeiHKeEh97SLUhn97tB1f
```

### Transactions by Block
```
  /silubium-api/txs/?block=HASH
  /silubium-api/txs/?block=00000000fa6cf7367e50ad14eb0ca4737131f256fc4c5841fd3c3f140140e6b6
```

### Transactions by Address
```
  /silubium-api/txs/?address=ADDR
  /silubium-api/txs/?address=mmhmMNfBiZZ37g1tgg2t8DDbNoEdqKVxAL
```

### Transactions Receipt
```
  /silubium-api/txs/[:tx_id]/receipt
```

### Transactions for Multiple Addresses
GET method:
```
  /silubium-api/addrs/[:addrs]/txs[?from=&to=]
  /silubium-api/addrs/2NF2baYuJAkCKo5onjUKEPdARSLUkZ6SYyKd5,2NAre8sX2povnjy4aeiHKeEh97SLUhn97tB1f/txs?from=0&to=20
```

POST method:
```
  /silubium-api/addrs/txs
```

POST params:
```
addrs: 2NF2baYuJAkCKo5onjUKEPdARSLUkZ6SYyKd5,2NAre8sX2povnjy4aeiHKeEh97SLUhn97tB1f
from (optional): 0
to (optional): 20
noAsm (optional): 1 (will omit script asm from results)
noScriptSig (optional): 1 (will omit the scriptSig from all inputs)
noSpent (option): 1 (will omit spent information per output)
```

Sample output:
```
{ totalItems: 100,
  from: 0,
  to: 20,
  items:
    [ { txid: '3e81723d069b12983b2ef694c9782d32fca26cc978de744acbc32c3d3496e915',
       version: 1,
       locktime: 0,
       vin: [Object],
       vout: [Object],
       blockhash: '00000000011a135e5277f5493c52c66829792392632b8b65429cf07ad3c47a6c',
       confirmations: 109367,
       time: 1393659685,
       blocktime: 1393659685,
       valueOut: 0.3453,
       size: 225,
       firstSeenTs: undefined,
       valueIn: 0.3454,
       fees: 0.0001 },
      { ... },
      { ... },
      ...
      { ... }
    ]
 }
```

Note: if pagination params are not specified, the result is an array of transactions.



### Transaction Broadcasting
POST method:
```
  /silubium-api/tx/send
```
POST params:
```
  rawtx: "signed transaction as hex string"

  eg

  rawtx: 01000000017b1eabe0209b1fe794124575ef807057c77ada2138ae4fa8d6c4de0398a14f3f00000000494830450221008949f0cb400094ad2b5eb399d59d01c14d73d8fe6e96df1a7150deb388ab8935022079656090d7f6bac4c9a94e0aad311a4268e082a725f8aeae0573fb12ff866a5f01ffffffff01f0ca052a010000001976a914cbc20a7664f2f69e5355aa427045bc15e7c6c77288ac00000000

```
POST response:
```
  {
      txid: [:txid]
  }

  eg

  {
      txid: "c7736a0a0046d5a8cc61c8c3c2821d4d7517f5de2bc66a966011aaa79965ffba"
  }
```

### Historic Blockchain Data Sync Status
```
  /silubium-api/sync
```

### Live Network P2P Data Sync Status
```
  /silubium-api/peer
```

### Status of the SILUBIUM Network
```
  /silubium-api/status?q=xxx
```
Where "xxx" can be:

 * getInfo
 * getDifficulty
 * getBestBlockHash
 * getLastBlockHash


### Utility Methods
```
  /silubium-api/utils/estimatefee[?nbBlocks=2]
```

### Min Estimate Fee Per KB
```
  /silubium-api/utils/minestimatefee[?nbBlocks=2]
```

resp:

```
{
    fee_per_kb: 0.00001
}
```

### SRC20 info
   
```
  /silubium-api/src20/:contractAddress
```

E.g.:
```
  `GET` /silubium-api/src20/0973e4b1598b5badf72076cb08727936f41ab40a
```

This would return:
```
{
  contract_address: "0973e4b1598b5badf72076cb08727936f41ab40a",
  total_supply: "1000000000000000000",
  decimals: "8",
  name: "WLToken",
  symbol: "WLT",
  version: "",
  transfers_count: 0,
  holders_count: 0,
  tx_hash: "4f349f09851c6e54291d468e95c9a182c30729b0d115810dfadacc8501efb6af",
  updated_at: "2018-08-13T01:27:05.546Z",
  block_height: 11682,
  contract_address_base: "SLUN9ywygdWW1pcVTtSHnsXTomehRhnduqL9",
  exception: false,
  created_at: "2018-08-13T01:27:05.546Z",
  tx_date_time: "2018-08-05T03:02:40.000Z",
  tx_time: 1533438160
}
```

### SRC20 transfers
```
  /silubium-api/src20/:contractAddress/transfers
```
* **SLUquery Params**

    * **Optional:**
        
            `limit=<Number>`
            
                > MAX_LIMIT === 100
            
            `offset=<Number>`
            
            `addresses=<Array.<String>>`

E.g.:
```
  `GET` /silubium-api/src20/0973e4b1598b5badf72076cb08727936f41ab40a/transfers?limit=20&offset=1&addresses[]=SLUZt8DT8u2JTyA8y37kKLWW79UfTFj7NXFS&addresses[]=SLUZt8DT8u2JTSD8y37kKLWW79UfTFj7NXFS
```

This would return:
```
{
limit: 100,
offset: 0,
count: 5,
items: [
          {
            contract_address: "0973e4b1598b5badf72076cb08727936f41ab40a",
            tx_hash: "9e3ff1f8062a22733c19954b3454ab28a47cdd6ba8bf315cc859ae6a3d454230",
            tx_time: 1535003776,
            from: "SLURN3UeTqRfrFrtS8NtXZgmZYqDLYPzfiC6",
            from_eth: "2ca435386a712b12c3e833e13c734bc946d77c4a",
            to: "SLUUnwhpqDSsAQknqWxENLEtv89kg9WJazaV",
            to_eth: "52422a58960b3e427ed957aa5cf8ed006db069d5",
            value: "1000000000"
          }
    ]
}
```

### SRC20 balances
```
  /silubium-api/src20/:contractAddress/balances
```

### Call Contract
```
/silubium-api/contracts/:contractaddress/hash/:contracthash/call
```

## Web Socket API

The web socket API is served using [socket.io](http://socket.io).

The following are the events published by silubium:

`tx`: new transaction received from network. This event is published in the 'inv' room. Data will be a app/models/Transaction object.
Sample output:
```
{
  "txid":"00c1b1acb310b87085c7deaaeba478cef5dc9519fab87a4d943ecbb39bd5b053",
  "processed":false
  ...
}
```


`block`: new block received from network. This event is published in the `inv` room. Data will be a app/models/Block object.
Sample output:
```
{
  "hash":"000000004a3d187c430cd6a5e988aca3b19e1f1d1727a50dead6c8ac26899b96",
  "time":1389789343,
  ...
}
```

`status`: every 1% increment on the sync task, this event will be triggered. This event is published in the `sync` room.

Sample output:
```
{
  blocksToSync: 164141,
  syncedBlocks: 475,
  upToExisting: true,
  scanningBackward: true,
  isEndGenesis: true,
  end: "000000000933ea01ad0ee984209779baaec3ced90fa3f408719526f8d77f4943",
  isStartGenesis: false,
  start: "000000009f929800556a8f3cfdbe57c187f2f679e351b12f7011bfc276c41b6d"
}
```

### Example Usage

The following html page connects to the socket.io silubium API and listens for new transactions.

html
```
<html>
<body>
  <script src="http://<silubium-server>:<port>/socket.io/socket.io.js"></script>
  <script>
    eventToListenTo = 'tx'
    room = 'inv'

    var socket = io("http://<silubium-server>:<port>/");
    socket.on('connect', function() {
      // Join the room.
      socket.emit('subscribe', room);
    })
    socket.on(eventToListenTo, function(data) {
      console.log("New transaction received: " + data.txid)
    })
  </script>
</body>
</html>
```

## License
(The MIT License)

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

