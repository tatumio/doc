# gettransactioninfobyblocknum

### How to use it

You can use the `getTransactionInfoByBlockNum` method with Tatum SDK by following the below example:

<pre class="language-typescript" data-overflow="wrap" data-line-numbers><code class="lang-typescript">// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

<strong>const transactionInfo = await tatum.rpc.getTransactionInfoByBlockNum(1000000)
</strong><strong>
</strong>await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
</code></pre>

Replace `1000000` with the actual block height that you want to get information about.

### Overview

The `getTransactionInfoByBlockNum` method allows you to query the TransactionInfo data of all transactions contained in the block of a specified height. This can be particularly useful when you need to track the status of all transactions within a particular block or analyse the transactions for auditing purposes.

{% embed url="https://codepen.io/tatum-devrel/pen/dyQLarr" %}

### Parameters

The `getTransactionInfoByBlockNum` method requires the following parameter:

* `num`: The block height you want to get transaction information about. It should be an integer.

### Return Object

Array of:

* `id`: The transaction ID (string)
* `fee`: The total number of TRX burned in this transaction, represented as an integer.
* `blockNumber`: The block number (integer)
* `blockTimeStamp`: The block timestamp, in milliseconds (integer)
* `contractResult`: Transaction execution results (string array)
* `contract_address`: Contract address (string)
* `receipt`: Transaction receipt, including transaction execution result and transaction fee details. It contains the following fields:
  * `energy_usage`: The amount of energy consumed in the caller's account
  * `energy_fee`: The amount of TRX burned to pay for energy
  * `origin_energy_usage`: The amount of energy consumed in the contract deployer's account
  * `energy_usage_total`: The total amount of energy consumed by the transaction
  * `net_usage`: The amount of bandwidth consumed
  * `net_fee`: The amount of TRX burned to pay for the bandwidth
  * `result`: Transaction execution result
  * `energy_penalty_total`: The amount of extra energy that needs to be paid for calling a few popular contracts
* `log`: The log of events triggered during the smart contract call.
* `result`: Execution results. If the execution is successful, the field will not be displayed in the returned value, if the execution fails, the field will be "FAILED"
* `resMessage`: When the transaction execution fails, the details of the failure will be returned through this field. Hex format, you can convert it to a string to get plaintext information.
* `withdraw_amount`: For the withdrawal reward transaction, unfreeze transaction, they will withdraw the vote reward to account. The number of rewards withdrawn to the account is returned through this field, and the unit is sun.
* `unfreeze_amount`: In the Stake1.0 stage, for unstaking transactions, this field returns the amount of unstaked TRX, the unit is sun.
* `internal_transactions`: Internal transaction
* `withdraw_expire_amount`: In the Stake2.0 stage, for unstaking transactions and withdrawing unfrozen balance transactions, this field returns the amount of unfrozen TRX withdrawn to the account in this transaction, the unit is sun.

### HTTP Request Example

```json
{
    "num": 1000000
}
```

### HTTP Response Example

```json
[
  {
    "log": [
      {
        "address": "7090190c41ba59f763e2cbe7d885e007e94be5d2",
        "data": "000000000000000000000000000000000000000000000000000000051f5e04fa0000000000000000000000000000000000000000000000000000000004a9681c0000000000000000000000000000000000000000000000000000000004a8fe4001000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000",
        "topics": [
          "baca790fd027b9b7f36b90c3084718a3a039693cdf83844342f5f1edc839c3af"
        ]
      }
    ],
    "blockNumber": 1000000,
    "contractResult": [
      ""
    ],
    "blockTimeStamp": 1578594852000,
    "receipt": {
      "result": "SUCCESS",
      "energy_usage": 124980,
      "energy_usage_total": 124980,
      "net_usage": 668
    },
    "id": "7faabd22623eb53467d34b2a417262f6df75433566c104b6c6eec5a227090df6",
    "contract_address": "417090190c41ba59f763e2cbe7d885e007e94be5d2"
  },
  {
    "log": [
      {
        "address": "8d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "data": "0000000000000000000000000000000000000000000000000000000001c890cf00000000000000000000000000000000000000000000000000000000000000150000000000000000000000000000000000000000000000000000000000000002",
        "topics": [
          "50b0fde04a05002ee4ba3c03973059b7d8af741148bf53ff213e39d2867a7930",
          "000000000000000000000000ed2f4270fa5a7cae1efd4706ae27a4335406921e"
        ]
      },
      {
        "address": "8d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "data": "0000000000000000000000000000000000000000000000000000000001cef96f",
        "topics": [
          "6a965f98da6f13a2ccafa10fd99074eb59617607c5c8153ceded5713e33c2cc1"
        ]
      },
      {
        "address": "8d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "data": "000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000050000000000000000000000000000000000000000000000000000000000d59f800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000290000000000000000000000000000000000000000000000000000000000000000",
        "topics": [
          "df1b2fae932fd98400d3d19f3d68900102b199899050d106565310ffd640c594",
          "000000000000000000000000ed2f4270fa5a7cae1efd4706ae27a4335406921e"
        ]
      }
    ],
    "fee": 433850,
    "blockNumber": 1000000,
    "contractResult": [
      "0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000500000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001500000000000000000000000000000000000000000000000000000000000000140000000000000000000000000000000000000000000000000000000001cef96f00000000000000000000000000000000000000000000000000000000000000290000000000000000000000000000000000000000000000000000000000000000"
    ],
    "blockTimeStamp": 1578594852000,
    "receipt": {
      "result": "SUCCESS",
      "energy_fee": 433850,
      "energy_usage_total": 43385,
      "net_usage": 384
    },
    "id": "98d0f4149bf8023a9df4d2b754f6c728a5b6d021c4497c6cd5452b97f01b0548",
    "contract_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
    "internal_transactions": [
      {
        "caller_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "note": "63616c6c",
        "transferTo_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "callValueInfo": [
          {}
        ],
        "hash": "ef89ade61942aa3371a3f006e6406fd4758ef648ee38c04f70a57b296668d3ed"
      },
      {
        "caller_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "note": "63616c6c",
        "transferTo_address": "413a5bfb715d2086ec513b64e98531e2f58154c44c",
        "callValueInfo": [
          {
            "callValue": 700000
          }
        ],
        "hash": "a630ff6999c4762637d5cecf109c55e225064bd11afcbb1ae301fbaa21cf3a78"
      }
    ]
  },
  {
    "log": [
      {
        "address": "79c23a5666042e40420d6afdc1541e3926205eba",
        "data": "000000000000000000000000000000000000000000000000000000051f5e04fa",
        "topics": [
          "678ae61fcbde3426947a5076f2541a6705fa78577e819a420c826e9c722ff792"
        ]
      }
    ],
    "blockNumber": 1000000,
    "contractResult": [
      ""
    ],
    "blockTimeStamp": 1578594852000,
    "receipt": {
      "result": "SUCCESS",
      "energy_usage": 28643,
      "energy_usage_total": 28643,
      "net_usage": 346
    },
    "id": "17e7321320bb08c40f027cbcca320152c2396c77a910f387849a944ee8aa0cb1",
    "contract_address": "4179c23a5666042e40420d6afdc1541e3926205eba",
    "internal_transactions": [
      {
        "caller_address": "4179c23a5666042e40420d6afdc1541e3926205eba",
        "note": "63616c6c",
        "transferTo_address": "4179c23a5666042e40420d6afdc1541e3926205eba",
        "callValueInfo": [
          {}
        ],
        "hash": "60b85ea10861cd2352f34de84fe72792fa9f02165f215f4432a54b152a30eb8e"
      }
    ]
  },
  {
    "log": [
      {
        "address": "8d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "data": "0000000000000000000000000000000000000000000000000000000001cef96f00000000000000000000000000000000000000000000000000000000000000030000000000000000000000000000000000000000000000000000000000000001",
        "topics": [
          "50b0fde04a05002ee4ba3c03973059b7d8af741148bf53ff213e39d2867a7930",
          "000000000000000000000000f07e117a4b5f1fda66f8fcedf44065f1dafc5ad7"
        ]
      },
      {
        "address": "8d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "data": "00000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000007622eb8000000000000000000000000000000000000000000000000000000000a9aba44200000000000000000000000000000000000000000000000000000000000000440000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000000000001f0000000000000000000000000000000000000000000000000000000000000000",
        "topics": [
          "df1b2fae932fd98400d3d19f3d68900102b199899050d106565310ffd640c594",
          "000000000000000000000000f07e117a4b5f1fda66f8fcedf44065f1dafc5ad7"
        ]
      }
    ],
    "fee": 376380,
    "blockNumber": 1000000,
    "contractResult": [
      "0000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000300000000000000000000000000000000000000000000000000000000a9aba4420000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000300000000000000000000000000000000000000000000000000000000000000140000000000000000000000000000000000000000000000000000000001cef96f000000000000000000000000000000000000000000000000000000000000001f0000000000000000000000000000000000000000000000000000000000000000"
    ],
    "blockTimeStamp": 1578594852000,
    "receipt": {
      "result": "SUCCESS",
      "energy_fee": 376380,
      "energy_usage_total": 37638,
      "net_usage": 385
    },
    "id": "4ef51a5760bf98dc2dd752658f48db1445e8ca75f8a6efe14d5a462a15edd3f0",
    "contract_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
    "internal_transactions": [
      {
        "caller_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "note": "63616c6c",
        "transferTo_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "callValueInfo": [
          {}
        ],
        "hash": "ebd48b28e91e23a0f190b2ef898c6c89d0723759eb17ceb9203fcd6a4b0b313e"
      },
      {
        "caller_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "note": "63616c6c",
        "transferTo_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "callValueInfo": [
          {}
        ],
        "hash": "4369d49d09a1d17cbff6a3c69e3bcd081f4c1d10fc176cab53371908e03819f1"
      },
      {
        "caller_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "note": "63616c6c",
        "transferTo_address": "41f07e117a4b5f1fda66f8fcedf44065f1dafc5ad7",
        "callValueInfo": [
          {
            "callValue": 2457950000
          }
        ],
        "hash": "b31eeb5d614133be49ff5be526d8bd258583b478c5daad9713b68591141b5f10"
      }
    ]
  },
  {
    "log": [
      {
        "address": "8d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "data": "0000000000000000000000000000000000000000000000000000000001cef96f000000000000000000000000000000000000000000000000000000000000000e0000000000000000000000000000000000000000000000000000000000000002",
        "topics": [
          "50b0fde04a05002ee4ba3c03973059b7d8af741148bf53ff213e39d2867a7930",
          "0000000000000000000000009ac63dd8e80daf0a786bf962860e2209b7fa5fb9"
        ]
      },
      {
        "address": "8d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "data": "0000000000000000000000000000000000000000000000000000000001d4027f",
        "topics": [
          "6a965f98da6f13a2ccafa10fd99074eb59617607c5c8153ceded5713e33c2cc1"
        ]
      },
      {
        "address": "8d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "data": "000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000050000000000000000000000000000000000000000000000000000000000a7d8c000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000014000000000000000000000000000000000000000000000000000000000000000300000000000000000000000000000000000000000000000000000000000000500000000000000000000000000000000000000000000000000000000000000000",
        "topics": [
          "df1b2fae932fd98400d3d19f3d68900102b199899050d106565310ffd640c594",
          "0000000000000000000000009ac63dd8e80daf0a786bf962860e2209b7fa5fb9"
        ]
      }
    ],
    "fee": 433850,
    "blockNumber": 1000000,
    "contractResult": [
      "0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000500000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000e00000000000000000000000000000000000000000000000000000000000000140000000000000000000000000000000000000000000000000000000001d4027f00000000000000000000000000000000000000000000000000000000000000500000000000000000000000000000000000000000000000000000000000000000"
    ],
    "blockTimeStamp": 1578594852000,
    "receipt": {
      "result": "SUCCESS",
      "energy_fee": 433850,
      "energy_usage_total": 43385,
      "net_usage": 384
    },
    "id": "80e07e3f2b92a0e9974b1398964e006288836dee82aa3a81e579a512e6581354",
    "contract_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
    "internal_transactions": [
      {
        "caller_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "note": "63616c6c",
        "transferTo_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "callValueInfo": [
          {}
        ],
        "hash": "3e32e3a6ef17975e8d2ac842a520cef987bf9d93d7c2538857b06d1c792da36e"
      },
      {
        "caller_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
        "note": "63616c6c",
        "transferTo_address": "413a5bfb715d2086ec513b64e98531e2f58154c44c",
        "callValueInfo": [
          {
            "callValue": 550000
          }
        ],
        "hash": "bc9897f79e4eaa5f795626b853a29baacb132283f5d0e6f94c0462894683cf9b"
      }
    ]
  },
  {
    "fee": 3130,
    "blockNumber": 1000000,
    "contractResult": [
      ""
    ],
    "blockTimeStamp": 1578594852000,
    "receipt": {
      "result": "SUCCESS",
      "net_fee": 3130,
      "energy_usage": 328466,
      "energy_usage_total": 328466
    },
    "id": "ba8e727c03d588619310d7a16a95fcfd31a516dbf8893ddd585e0bbd7e0deae4",
    "contract_address": "41174e91a57d68f5ac1bc485d03a038fe745a3b89b"
  }
]
```
