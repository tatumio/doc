# eth\_getTransactionReceipt

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
<pre class="language-typescript" data-overflow="wrap" data-line-numbers><code class="lang-typescript">// yarn add @tatumio/tatum

import { TatumSDK, Chiliz, Network} from '@tatumio/tatum'
  
const tatum = await TatumSDK.init&#x3C;HorizenEon>({network: Network.Chiliz})

<strong>const tx = await tatum.rpc.getTransactionReceipt('0x97d83656ca05890100149be18d0c2a2f94e5337e5e6a643ea78794cd418cdbc7')
</strong>
tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
</code></pre>
{% endtab %}

{% tab title="C#" %}
```csharp
// dotnet add ${your_project} package Tatum

var tatumSdk = await TatumSdk.InitAsync();

var rpcCall = new JsonRpcCall
{
    Id = "1",
    JsonRpc = "2.0",
    Method = "eth_getTransactionReceipt",
    Params = new object[] 
    {
        "0xa536596d043c03d709aaccbc53f421963fe3537274e86444cd984404cf9ecb13"
    }
};

var result = await tatumSdk.Rpc.Eon.Call(rpcCall);
```
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionReceipt` is an JSON-RPC method that retrieves the transaction receipt of a given transaction hash. This method is particularly useful when you need to obtain detailed information about a transaction's execution, such as its status (success or failure), gas usage, and logs (events). Common use cases include checking the status of a transaction after it has been mined or inspecting the events emitted by a smart contract during a specific transaction.

### Parameters

This method requires a single parameter:

* **`transactionHash`**: The hash of the transaction for which you want to obtain the receipt.
  * Example: `"0x97d83656ca05890100149be18d0c2a2f94e5337e5e6a643ea78794cd418cdbc7"`

### Return Object

The method returns an object containing the following fields:

* **`transactionHash`**: The hash of the transaction.
* **`transactionIndex`**: The transaction's index position in the block.
* **`blockHash`**: The hash of the block where this transaction was mined.
* **`blockNumber`**: The block number where this transaction was mined.
* **`from`**: The address of the sender.
* **`to`**: The address of the receiver. `null` when it's a contract creation transaction.
* **`cumulativeGasUsed`**: The total amount of gas used when this transaction was executed in the block.
* **`gasUsed`**: The amount of gas used by this specific transaction alone.
* **`contractAddress`**: The address of the contract created, if the transaction was a contract creation. Otherwise, `null`.
* **`logs`**: An array of log objects, which were emitted during the transaction.
* **`logsBloom`**: A 256-byte bloom filter, which is a compressed representation of the logs emitted during the transaction.
* **`status`**: The status of the transaction's execution. `"0x1"` indicates success, while `"0x0"` indicates failure.

### JSON-RPC Examples

Request:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "eth_getTransactionReceipt",
  "params": [
    "0x97d83656ca05890100149be18d0c2a2f94e5337e5e6a643ea78794cd418cdbc7"
  ]
}
```

Response:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "blockHash": "0xb0ddfcdcc375afce9f365458c5035ca4aaf99f9fe8699522193e16a8718615b6",
    "blockNumber": "0x5a9d4",
    "transactionIndex": "0x0",
    "transactionHash": "0x97d83656ca05890100149be18d0c2a2f94e5337e5e6a643ea78794cd418cdbc7",
    "type": "0x2",
    "from": "0x8bd5723981d3f96a6544519c4a075f5994919d3a",
    "to": "0xa55d9ef16af921b70fed1421c1d298ca5a3a18f1",
    "effectiveGasPrice": "0x5017ff700",
    "contractAddress": null,
    "logs": [],
    "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "gasUsed": "0x12a68",
    "cumulativeGasUsed": "0x12a68",
    "status": "0x1"
  }
}
```

\
