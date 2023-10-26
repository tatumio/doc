# eth\_getBalance

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const balance = await tatum.rpc.getBalance('0x742d35Cc6634C0532925a3b844Bc454e4438f44e')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_getBalance` method is an Ethereum JSON-RPC method that allows you to retrieve the Ether balance of a specified address. This method can be used to query the balance of any Ethereum address, whether it is a contract or an externally owned account (EOA). A common use case for this method is to display the current balance of a user's account in a wallet application or a decentralised application (DApp).

{% embed url="https://codepen.io/tatum-devrel/pen/qBQgNWd" %}
Try this feature
{% endembed %}

### Parameters

The method requires two parameters:

1. **`address`** (required): The address of the account or contract whose balance you want to query.
   * Example: `"0x742d35Cc6634C0532925a3b844Bc454e4438f44e"`
2. **`blockParameter`** (optional): The block number or block identifier to specify the point in time for which you want to query the balance.
   * Example: `"latest"` or `"0x1"`

#### Transaction Details

For the purpose of this documentation, we'll also describe the `transactions` field of a full transaction object. The `eth_getBalance` method does not return transaction details, but we provide this information for completeness.

A full transaction object includes the following fields:

* **`hash`**: The transaction hash.
* **`nonce`**: The number of transactions made by the sender prior to this one.
* **`blockHash`**: The hash of the block in which the transaction was included.
* **`blockNumber`**: The block number in which the transaction was included.
* **`transactionIndex`**: The index of the transaction in the block.
* **`from`**: The sender's address.
* **`to`**: The recipient's address (or `null` for contract creation transactions).
* **`value`**: The value transferred, in wei.
* **`gasPrice`**: The gas price provided by the sender, in wei.
* **`gas`**: The maximum gas allowed for the transaction.
* **`input`**: The data sent with the transaction (typically for contract interaction).
* **`v`**, **`r`**, **`s`**: The raw signature values of the transaction.

### Return Object

The method returns a single field:

* `result`: The Ether balance of the specified address in wei, as a hexadecimal string.
  * Example: `"0x1a2e1a"`, which corresponds to `1,726,666` wei.

### JSON-RPC Request and Response Examples

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "eth_getBalance",
  "params": [
    "0x742d35Cc6634C0532925a3b844Bc454e4438f44e",
    "latest"
  ]
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x1a2e1a"
}
```
