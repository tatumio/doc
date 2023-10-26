# getblockbylatestnum

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getBlockByLatestNum(5)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getBlockByLatestNum` method retrieves a specified number of the most recent blocks from the TRON blockchain. This can be helpful when you need to analyse or display recent blockchain data.

{% embed url="https://codepen.io/tatum-devrel/pen/ExOJrGL" %}

### Parameters

* `num` (integer): The number of the most recent blocks to retrieve.

### Return Object

* `block:` Array of blocks
  *
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
  "num": 5
}
```

### HTTP Response Example

```json
{
  "block": [
    {
      "blockID": "000000000203c375c7521ef953106e9a112e1902664a91becc5f40371a7397d7",
      "block_header": {
        "raw_data": {
          "number": 33801077,
          "txTrieRoot": "30fe6502e11e110fa389d5c17e1cf53fa8df93f26297d9f27cd8c07d3558d722",
          "witness_address": "41e71c365c9dbf284ca8c1eed2d7877638941b9011",
          "parentHash": "000000000203c3741f9a08f594934bd26df95cc6c49b475d118e3a87aed5a4a4",
          "version": 27,
          "timestamp": 1684509309000
        },
        "witness_signature": "cb4845bbd745f620852a1a54a955cee0d1aecc209f2f96e9b4ea53bf3d2ceb0f665fa07a5e870fcf9c6b98110a33d5bba5f35b588cc4123394b7e9f439fe265301"
      },
      "transactions": [
        {
          "ret": [
            {
              "contractRet": "SUCCESS"
            }
          ],
          "signature": [
            "95874b4774ba56125dfd7bf2a99a0652d4abda98c6977e3f417852b7ea6f2b81ff2f260df473d186be9586b6bbeb74b5382d7f058593fd72fb60da5d0f77f77100"
          ],
          "txID": "31370141e3345421bdb92eff72f0d69aba8d04e636317ed52745d3f97e9faabb",
          "raw_data": {
            "contract": [
              {
                "parameter": {
                  "value": {
                    "data": "37383d0e00000000000000000000000000000000000000000000000000000188349354c9",
                    "owner_address": "41fcf7ab2a2fb29362babd41647a22b223f7fbedec",
                    "contract_address": "41c3c5115bd3f5cfe5559c634eeb250f339ae3e29c"
                  },
                  "type_url": "type.googleapis.com/protocol.TriggerSmartContract"
                },
                "type": "TriggerSmartContract"
              }
            ],
            "ref_block_bytes": "c362",
            "ref_block_hash": "4ddf60f936a910d9",
            "expiration": 1684509366000,
            "fee_limit": 150000000,
            "timestamp": 1684509306936
          },
          "raw_data_hex": "0a02c36222084ddf60f936a910d940f0add4a483315a8e01081f1289010a31747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e54726967676572536d617274436f6e747261637412540a1541fcf7ab2a2fb29362babd41647a22b223f7fbedec121541c3c5115bd3f5cfe5559c634eeb250f339ae3e29c222437383d0e00000000000000000000000000000000000000000000000000000188349354c970b8e0d0a48331900180a3c347"
        }
      ]
    },
    {
      "blockID": "000000000203c376d3d45ca88309982517d69ff0ec4d9a9f9f25536cebcdd76b",
      "block_header": {
        "raw_data": {
          "number": 33801078,
          "txTrieRoot": "0000000000000000000000000000000000000000000000000000000000000000",
          "witness_address": "41e61626ef01662b320a8ba38372e9db9cca940a3b",
          "parentHash": "000000000203c375c7521ef953106e9a112e1902664a91becc5f40371a7397d7",
          "version": 27,
          "timestamp": 1684509312000
        },
        "witness_signature": "f38e08044df52f0bd3314a0dc73431290c323e20a67297da8be939041a8eae484e1094ba455c78b71f198bfaf80aee68bb5e9d40f9146158e88ed776d2034e9800"
      }
    },
    {
      "blockID": "000000000203c3772b4f36792ea4f44a6d8345ccacee8a00d6f309a206193f1c",
      "block_header": {
        "raw_data": {
          "number": 33801079,
          "txTrieRoot": "0000000000000000000000000000000000000000000000000000000000000000",
          "witness_address": "41e76da262ad1ca05274f74258ee18bc7fcc4987dc",
          "parentHash": "000000000203c376d3d45ca88309982517d69ff0ec4d9a9f9f25536cebcdd76b",
          "version": 27,
          "timestamp": 1684509315000
        },
        "witness_signature": "c6413a9d83553d6243eff19c27c136436e9e2e1b2315849e71232ae473614fdf3034ce215c8695c7ca15742899dcf6c276b3be918b6b8049b74f3b81a3c695b500"
      }
    },
    {
      "blockID": "000000000203c378d7df0f9d0edecc8b5e7edac57543e6fa421bbae6b1448e5f",
      "block_header": {
        "raw_data": {
          "number": 33801080,
          "txTrieRoot": "0000000000000000000000000000000000000000000000000000000000000000",
          "witness_address": "41290bf92b578a1c615ebb273aff6a285230c02f65",
          "parentHash": "000000000203c3772b4f36792ea4f44a6d8345ccacee8a00d6f309a206193f1c",
          "version": 27,
          "timestamp": 1684509318000
        },
        "witness_signature": "122a4463f64743b90f1e0f476bd878aae576225591643972595a7bb250ddee2757287b8c8ab627ba95e027e55421160ea2b6bb543bcaa89b871427113bbab6a101"
      }
    },
    {
      "blockID": "000000000203c3799526a98bab56861511f0e67ec65557826d7bfc0b36e17450",
      "block_header": {
        "raw_data": {
          "number": 33801081,
          "txTrieRoot": "0000000000000000000000000000000000000000000000000000000000000000",
          "witness_address": "41977f82c69011cf4a7db6f7339edcded85c614d45",
          "parentHash": "000000000203c378d7df0f9d0edecc8b5e7edac57543e6fa421bbae6b1448e5f",
          "version": 27,
          "timestamp": 1684509321000
        },
        "witness_signature": "bd07babfec59340828d6d82032a0865f22391df29c43647c0e3186e21b9df43d2f78f3cb50d4a0113f08ebd7c02663ffc169352297256cce4bd62b04a4289e1d01"
      }
    }
  ]
}
```
