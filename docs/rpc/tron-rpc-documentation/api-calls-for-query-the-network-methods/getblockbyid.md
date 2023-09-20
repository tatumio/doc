# getblockbyid

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getBlockById('000000000326bcabea2fa533c7080c8baf231f320d3ccdd54a59e3fcb1760364')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getBlockById` method allows you to query a specific block on the TRON blockchain by providing the block's ID. This can be useful when you want to retrieve specific transactional or metadata about a particular block.

### Parameters

* `value` (string): The ID of the block to query. This is the block hash which uniquely identifies each block on the TRON blockchain.

### Return Object

* `blockID` (string): The block hash.
* `block_header` (object)
  * `raw_data` (object)
    * `timestamp` (integer): The timestamp of the block.
    * `txTrieRoot` (string): The root of the transaction merkle tree.
    * `parentHash` (string): The parent block hash.
    * `number` (integer): The block number.
    * `witness_id` (integer): The witness id.
    * `witness_address` (string): The witness address.
    * `version` (integer): The version.
    * `accountStateRoot` (string): The root of the account state tree.
  * `witness_signature` (string): The signature of the Super Representative (SR).
* `transactions` (Array): Contains transaction information in the block.
  * `raw_data.contract` - The main content of the transaction, contract is a list, but only one element is used at present. Different types of transactions have different contract contents. For example, for a TRX transfer type transaction, the contract will include the transfer amount, receiver address and other information. TRON supports multiple types of contracts, please refer to the official documentation [Types of Transaction](https://developers.tron.network/docs/tron-protocol-transaction#types-of-transaction).
  * `raw_data.ref_block_bytes` - The height of the transaction reference block, using the 6th to 8th (exclusive) bytes of the reference block height, a total of 2 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
  * `raw_data.ref_block_hash` - The hash of the transaction reference block, using the 8th to 16th (exclusive) bytes of the reference block hash, a total of 8 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
  * `raw_data.expiration` - Transaction expiration time, beyond which the transaction will no longer be packed. If the transaction is created by calling the java-tron API, its expiration time will be automatically set by the node to the value of adding 60 seconds to the timestamp of the node's latest block. The expiration time interval can be modified in the node's configuration file, the maximum value cannot exceed 24 hours.
  * `raw_data.data` - Transaction memo.
  * `raw_data.timestamp` - Transaction timestamp, set as the transaction creation time.
  * `raw_data.fee_limit` - The maximum energy cost allowed for the execution of smart contract transactions. Only deploying and triggering smart contract transactions need to be set, others not.
  * `signature` - The sender's signature for the transaction. This proves that the transaction could only have come from the sender and was not sent fraudulently.
  * `txID` - transaction id

### HTTP Request Example

```json
{
 "value": "0x000000000332a91b74ac983b698b9b6ddb087631992fcf8a4cf838b8500e7767"
}
```

### HTTP Response Example

```json
{
  "blockID": "00000000000f424013e51b18e0782a32fa079ddafdb2f4c343468cf8896dc887",
  "block_header": {
    "raw_data": {
      "number": 1000000,
      "txTrieRoot": "e2dd42daa9c853e070df1e4fc927851a7438c601fb12cf945922629d5cec187b",
      "witness_address": "41f16412b9a17ee9408646e2a21e16478f72ed1e95",
      "parentHash": "00000000000f423fbccd9cdb9e410eabdf9f94145cf5b71a678b8b9616619125",
      "version": 9,
      "timestamp": 1578594852000
    },
    "witness_signature": "179caed28b3d129dee6d553ae6761a8c8698f890e5f38e062d56e2d0d0b8c9a20317b7753b3fd1be261935d6182434a6c057f8926f25027b9859cde3da3a655300"
  },
  "transactions": [
    {
      "ret": [
        {
          "contractRet": "SUCCESS"
        }
      ],
      "signature": [
        "95428ed2e263600933f82bf67f43e15450bc2da3b7b2987a7f46b0b9b9c4aae7ba5ea005b9297fbff5bca5fe5c9b05299433e36e10224c167f9c613b6dded39000"
      ],
      "txID": "7faabd22623eb53467d34b2a417262f6df75433566c104b6c6eec5a227090df6",
      "raw_data": {
        "contract": [
          {
            "parameter": {
              "value": {
                "data": "ae21db6f0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000051f5e04fa0000000000000000000000000000000000000000000000000000000004a9681c0000000000000000000000000000000000000000000000000000000004a8fe400000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000051f5e04f9000000000000000000000000000000000000000000000000000000051f5e04f8000000000000000000000000000000000000000000000000000000051f5e04f7000000000000000000000000000000000000000000000000000000051f5e04f6000000000000000000000000000000000000000000000000000000051f5e04f5000000000000000000000000000000000000000000000000000000051f5e04f4000000000000000000000000000000000000000000000000000000051f5e04f3",
                "owner_address": "41920bb75dd5751afd68e1d55a8a0bc1bc39b32c78",
                "contract_address": "417090190c41ba59f763e2cbe7d885e007e94be5d2"
              },
              "type_url": "type.googleapis.com/protocol.TriggerSmartContract"
            },
            "type": "TriggerSmartContract"
          }
        ],
        "ref_block_bytes": "423e",
        "ref_block_hash": "5c35fda2f1a9a386",
        "expiration": 1578594906000,
        "fee_limit": 1000000000,
        "timestamp": 1578594849159
      },
      "raw_data_hex": "0a02423e22085c35fda2f1a9a3864090dfdadcf82d5af003081f12eb030a31747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e54726967676572536d617274436f6e747261637412b5030a1541920bb75dd5751afd68e1d55a8a0bc1bc39b32c781215417090190c41ba59f763e2cbe7d885e007e94be5d2228403ae21db6f0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000051f5e04fa0000000000000000000000000000000000000000000000000000000004a9681c0000000000000000000000000000000000000000000000000000000004a8fe400000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000051f5e04f9000000000000000000000000000000000000000000000000000000051f5e04f8000000000000000000000000000000000000000000000000000000051f5e04f7000000000000000000000000000000000000000000000000000000051f5e04f6000000000000000000000000000000000000000000000000000000051f5e04f5000000000000000000000000000000000000000000000000000000051f5e04f4000000000000000000000000000000000000000000000000000000051f5e04f37087a3d7dcf82d90018094ebdc03"
    },
    {
      "ret": [
        {
          "contractRet": "SUCCESS"
        }
      ],
      "signature": [
        "6e3f72c5d8bf433bf98ac3bbcdfbbb179d8cd8f5f6da5f1eb0466bbc80bcebee6dc0e5312796c37c3fe73d49f9b350cf61f4830deb7d846c90570f8afb3f513400"
      ],
      "txID": "98d0f4149bf8023a9df4d2b754f6c728a5b6d021c4497c6cd5452b97f01b0548",
      "raw_data": {
        "contract": [
          {
            "parameter": {
              "value": {
                "data": "0204b01b000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000001000000000000000000000000db4df489cf3977fbf0d06e47885f3dc85446b4aa",
                "owner_address": "41ed2f4270fa5a7cae1efd4706ae27a4335406921e",
                "contract_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
                "call_value": 14000000
              },
              "type_url": "type.googleapis.com/protocol.TriggerSmartContract"
            },
            "type": "TriggerSmartContract"
          }
        ],
        "ref_block_bytes": "423f",
        "ref_block_hash": "bccd9cdb9e410eab",
        "expiration": 1578594909000,
        "fee_limit": 1000000000,
        "timestamp": 1578594849385
      },
      "raw_data_hex": "0a02423f2208bccd9cdb9e410eab40c8f6dadcf82d5ad401081f12cf010a31747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e54726967676572536d617274436f6e74726163741299010a1541ed2f4270fa5a7cae1efd4706ae27a4335406921e1215418d9dd663cf90256fdf2faba2a1be71f8a0147f8c1880bfd60622640204b01b000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000001000000000000000000000000db4df489cf3977fbf0d06e47885f3dc85446b4aa70e9a4d7dcf82d90018094ebdc03"
    },
    {
      "ret": [
        {
          "contractRet": "SUCCESS"
        }
      ],
      "signature": [
        "230b8767e8745d01f38d2b9f742f4037eb81e93bcc9c2d60bedf4bab3b9e0c16692138a112f1610b505cf3109f3a5ff00d6687c09b3c94a734dd8aedfc92d82101"
      ],
      "txID": "17e7321320bb08c40f027cbcca320152c2396c77a910f387849a944ee8aa0cb1",
      "raw_data": {
        "contract": [
          {
            "parameter": {
              "value": {
                "data": "f6d4ef1a0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000051f5e04fa",
                "owner_address": "41920bb75dd5751afd68e1d55a8a0bc1bc39b32c78",
                "contract_address": "4179c23a5666042e40420d6afdc1541e3926205eba"
              },
              "type_url": "type.googleapis.com/protocol.TriggerSmartContract"
            },
            "type": "TriggerSmartContract"
          }
        ],
        "ref_block_bytes": "423e",
        "ref_block_hash": "5c35fda2f1a9a386",
        "expiration": 1578594906000,
        "fee_limit": 1000000000,
        "timestamp": 1578594849187
      },
      "raw_data_hex": "0a02423e22085c35fda2f1a9a3864090dfdadcf82d5aae01081f12a9010a31747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e54726967676572536d617274436f6e747261637412740a1541920bb75dd5751afd68e1d55a8a0bc1bc39b32c7812154179c23a5666042e40420d6afdc1541e3926205eba2244f6d4ef1a0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000051f5e04fa70a3a3d7dcf82d90018094ebdc03"
    },
    {
      "ret": [
        {
          "contractRet": "SUCCESS"
        }
      ],
      "signature": [
        "55124a9bfb733a27fc193b00c9c2ce0c1f969ffd0ec59c295fea00a75501206b0d5333c16c8f6a5aa7a32a03268edd3ca903d41f386001733a7d0199bcedb8bb01"
      ],
      "txID": "4ef51a5760bf98dc2dd752658f48db1445e8ca75f8a6efe14d5a462a15edd3f0",
      "raw_data": {
        "contract": [
          {
            "parameter": {
              "value": {
                "data": "0204b01b00000000000000000000000000000000000000000000000000000000000000440000000000000000000000000000000000000000000000000000000000000003000000000000000000000000db4df489cf3977fbf0d06e47885f3dc85446b4aa",
                "owner_address": "41f07e117a4b5f1fda66f8fcedf44065f1dafc5ad7",
                "contract_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
                "call_value": 1982000000
              },
              "type_url": "type.googleapis.com/protocol.TriggerSmartContract"
            },
            "type": "TriggerSmartContract"
          }
        ],
        "ref_block_bytes": "423f",
        "ref_block_hash": "bccd9cdb9e410eab",
        "expiration": 1578594909000,
        "fee_limit": 1000000000,
        "timestamp": 1578594850315
      },
      "raw_data_hex": "0a02423f2208bccd9cdb9e410eab40c8f6dadcf82d5ad501081f12d0010a31747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e54726967676572536d617274436f6e7472616374129a010a1541f07e117a4b5f1fda66f8fcedf44065f1dafc5ad71215418d9dd663cf90256fdf2faba2a1be71f8a0147f8c1880d78bb10722640204b01b00000000000000000000000000000000000000000000000000000000000000440000000000000000000000000000000000000000000000000000000000000003000000000000000000000000db4df489cf3977fbf0d06e47885f3dc85446b4aa708bacd7dcf82d90018094ebdc03"
    },
    {
      "ret": [
        {
          "contractRet": "SUCCESS"
        }
      ],
      "signature": [
        "153d437be2c417d88bef564a1421d2c3debb9f3828e9276a58578eb566091d6a612d3294c124ba3a5da37815d49b7cc7a91be04c0304a8e9ecee02f4d3dc420901"
      ],
      "txID": "80e07e3f2b92a0e9974b1398964e006288836dee82aa3a81e579a512e6581354",
      "raw_data": {
        "contract": [
          {
            "parameter": {
              "value": {
                "data": "0204b01b00000000000000000000000000000000000000000000000000000000000000140000000000000000000000000000000000000000000000000000000000000003000000000000000000000000db4df489cf3977fbf0d06e47885f3dc85446b4aa",
                "owner_address": "419ac63dd8e80daf0a786bf962860e2209b7fa5fb9",
                "contract_address": "418d9dd663cf90256fdf2faba2a1be71f8a0147f8c",
                "call_value": 11000000
              },
              "type_url": "type.googleapis.com/protocol.TriggerSmartContract"
            },
            "type": "TriggerSmartContract"
          }
        ],
        "ref_block_bytes": "423f",
        "ref_block_hash": "bccd9cdb9e410eab",
        "expiration": 1578594909000,
        "fee_limit": 1000000000,
        "timestamp": 1578594851357
      },
      "raw_data_hex": "0a02423f2208bccd9cdb9e410eab40c8f6dadcf82d5ad401081f12cf010a31747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e54726967676572536d617274436f6e74726163741299010a15419ac63dd8e80daf0a786bf962860e2209b7fa5fb91215418d9dd663cf90256fdf2faba2a1be71f8a0147f8c18c0b19f0522640204b01b00000000000000000000000000000000000000000000000000000000000000140000000000000000000000000000000000000000000000000000000000000003000000000000000000000000db4df489cf3977fbf0d06e47885f3dc85446b4aa709db4d7dcf82d90018094ebdc03"
    },
    {
      "ret": [
        {
          "contractRet": "SUCCESS"
        }
      ],
      "signature": [
        "a2e6784005b0bd9f80dcb92de8f37133e3355a09496bd7467580805226e2ed520e48858456151dc681e423f0041ae877369a16e6d805facc7af9d27b712891bb01"
      ],
      "txID": "ba8e727c03d588619310d7a16a95fcfd31a516dbf8893ddd585e0bbd7e0deae4",
      "raw_data": {
        "contract": [
          {
            "parameter": {
              "value": {
                "data": "8a157bf900000000000000000000000000000000000000000000000000000000000019be",
                "owner_address": "4141c910d7942636ae041975616104ef253e5a8371",
                "contract_address": "41174e91a57d68f5ac1bc485d03a038fe745a3b89b"
              },
              "type_url": "type.googleapis.com/protocol.TriggerSmartContract"
            },
            "type": "TriggerSmartContract"
          }
        ],
        "ref_block_bytes": "423f",
        "ref_block_hash": "bccd9cdb9e410eab",
        "expiration": 1578594909000,
        "fee_limit": 10000000,
        "timestamp": 1578594850984
      },
      "raw_data_hex": "0a02423f2208bccd9cdb9e410eab40c8f6dadcf82d5a8e01081f1289010a31747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e54726967676572536d617274436f6e747261637412540a154141c910d7942636ae041975616104ef253e5a8371121541174e91a57d68f5ac1bc485d03a038fe745a3b89b22248a157bf900000000000000000000000000000000000000000000000000000000000019be70a8b1d7dcf82d900180ade204"
    }
  ]
}
```
