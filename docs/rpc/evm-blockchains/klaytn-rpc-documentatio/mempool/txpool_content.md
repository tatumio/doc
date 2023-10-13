# txpool\_content

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Klaytn, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Klaytn>({network: Network.KLAYTN})

const content = await tatum.rpc.txPoolContent()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `txpool_content` method provides information about the transactions currently pending in the transaction pool of the Flare node. It can be helpful for developers and node operators to monitor and manage the transaction pool, especially in scenarios where it's necessary to analyze transaction congestion or prioritize specific transactions.

Use cases for the `txpool_content` method include:

* Analyzing network congestion by inspecting the transaction pool
* Prioritizing transactions by gas price
* Monitoring transactions from specific addresses
* Debugging and troubleshooting pending transactions

### Parameters

This method does not require any parameters.

### Return Object

The `txpool_content` method returns an object with two fields: `pending` and `queued`. Each field contains a nested object with addresses as keys and their respective transactions as values.

* **`pending`**: An object containing transactions that are currently pending for inclusion in the next block(s).
* **`queued`**: An object containing transactions that are currently queued (i.e., transactions that do not meet certain criteria for inclusion in the next block, like low gas price or nonce gaps).

Each transaction object includes the following information:

* **`hash`**: The hash of the transaction (32 bytes).
* **`nonce`**: The number of transactions sent by the sender prior to this one (integer).
* **`blockHash`**: The hash of the block in which the transaction was included (32 bytes), or `null` if the transaction is not yet mined.
* **`blockNumber`**: The block number in which the transaction was included (integer), or `null` if the transaction is not yet mined.
* **`transactionIndex`**: The index of the transaction in the block (integer), or `null` if the transaction is not yet mined.
* **`from`**: The address of the sender (20 bytes).
* **`to`**: The address of the receiver (20 bytes), or `null` for contract creation transactions.
* **`value`**: The value transferred in the transaction, in wei.
* **`gasPrice`**: The price of gas for the transaction, in wei.
* **`maxFeePerGas`** - The maximum fee per gas set in the transaction.
* **`maxPriorityFeePerGas`** - The maximum priority gas fee set in the transaction.
* **`gas`**: The maximum amount of gas the transaction is allowed to consume.
* **`input`**: The data payload of the transaction (string), or `0x` for simple value transfers.

### JSON-RPC Request Example

```json
jsonCopy code{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "txpool_content",
  "params": []
}
```

### JSON-RPC Response Example

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "pending": {
            "0x01d3B93AaADE8A4066DAaBc8fd8482173A6aD120": {
                "197": {
                    "blockHash": null,
                    "blockNumber": null,
                    "from": "0x01d3b93aaade8a4066daabc8fd8482173a6ad120",
                    "gas": "0x1c9c380",
                    "gasPrice": "0x16cf917",
                    "maxFeePerGas": "0x16cf917",
                    "maxPriorityFeePerGas": "0x16cf917",
                    "hash": "0x1da9c2a8f0787bac4747c5ed1035e81f6a6745aeea43943e63635fc367b817f7",
                    "input": "0x00000000",
                    "nonce": "0xc5",
                    "to": "0x4f023eb8c6bc3116e35b67e03bf2c17f2e4f7e7e",
                    "transactionIndex": null,
                    "value": "0x0",
                    "type": "0x2",
                    "accessList": [],
                    "chainId": "0xaa36a7",
                    "v": "0x1",
                    "r": "0x14f7578b57fd9f87acf5bbceb0a47f2d2d3f39b49169357457618c9634c45e8a",
                    "s": "0x775fa9976c571751a79f069f8c96f6489f286246e157a31fa99b33062631b46d"
                }
            }
        },
        "queued": {
            "0x03321406635a04D37Cf9211F2ea3AFc83a87e777": {
                "5096281": {
                    "blockHash": null,
                    "blockNumber": null,
                    "from": "0x03321406635a04d37cf9211f2ea3afc83a87e777",
                    "gas": "0x5208",
                    "gasPrice": "0xc570bd200",
                    "hash": "0x05f5fb8e46793fafdc924917c0afdd0afb4a53cb562542d5399234bc1eff759b",
                    "input": "0x",
                    "nonce": "0x4dc359",
                    "to": "0x77b1c86ab0aa9066803ed567e1f00973976638f6",
                    "transactionIndex": null,
                    "value": "0xb1a2b96602aa20",
                    "type": "0x0",
                    "chainId": "0xaa36a7",
                    "v": "0x1546d72",
                    "r": "0x62bd220b95ec13827c0d9b643b9beaf6f4c66d4a8ef08bb10f93d5e5c7ae0068",
                    "s": "0x467f76847cfdf43a002defe054030c1a88a9e6f56539c051c3cba46b2dd2cc89"
                }
            }
        }
    }
```

\
