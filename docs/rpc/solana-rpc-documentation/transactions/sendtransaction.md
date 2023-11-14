# sendTransaction

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const transaction = '4hXTCkRzt9WyecNzV1XPgCDfGAZzQKNxLXgynz5QDuWWPSAZBZSHptvWRL3BjCvzUXRdKvHL2b7yGrRQcWyaqsaBCncVG7BFggS8w9snUts67BSh3EqKpXLUm5UMHfD7ZBe9GhARjbNQMLJ1QD3Spr6oMTBU6EhdB4RD8CP2xUxr2u3d6fos36PD98XS6oX8TQjLpsMwncs5DAMiD4nNnR8NBfyghGCWvCVifVwvA8B8TJxE1aiyiv2L429BCWfyzAme5sZW8rDb14NeCQHhZbtNqfXhcp2tAnaAT'
const options = {
  encoding: Encoding.Base58,
  skipPreflight: false,
  preflightCommitment: Commitment.Finalized,
  maxRetries: 5,
  minContextSlot: 10
} // optional

const res = await tatum.rpc.sendTransaction(transaction, options)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `sendTransaction` method is used to submit a fully signed transaction to the cluster for processing. This method does not alter the transaction in any way; it relays the transaction created by clients to the node as-is. A successful response from this method does not guarantee the transaction is processed or confirmed by the cluster.&#x20;

While the rpc service will reasonably retry to submit it, the transaction could be rejected if transaction's `recent_blockhash` expires before it lands.

Use `getSignatureStatuses` to ensure a transaction is processed and confirmed.

Before submitting, the following preflight checks are performed:

1. The transaction signatures are verified
2. The transaction is simulated against the bank slot specified by the preflight commitment. On failure an error will be returned. Preflight checks may be disabled if desired. It is recommended to specify the same commitment and preflight commitment to avoid confusing behaviour.

The returned signature is the first signature in the transaction, which is used to identify the transaction (transaction id). This identifier can be easily extracted from the transaction data before submission.

### Parameters

* `transaction`(string, required): Fully-signed Transaction, as an encoded string.
  * Example: `'4hXTCkRzt9WyecNzV1XPgCDfGAZzQKNxLXgynz5QDuWWPSAZBZSHptvWRL3BjCvzUXRdKvHL2b7yGrRQcWyaqsaBCncVG7BFggS8w9snUts67BSh3EqKpXLUm5UMHfD7ZBe9GhARjbNQMLJ1QD3Spr6oMTBU6EhdB4RD8CP2xUxr2u3d6fos36PD98XS6oX8TQjLpsMwncs5DAMiD4nNnR8NBfyghGCWvCVifVwvA8B8TJxE1aiyiv2L429BCWfyzAme5sZW8rDb14NeCQHhZbtNqfXhcp2tAnaAT'`
* `options` (object, optional): An object containing various options for the request.
  * `encoding` (string, optional): Encoding used for the transaction data.&#x20;
    * Values: `base58` (_slow_, **DEPRECATED**), or `base64`.
  * `skipPreflight` (boolean, optional): If "true", skip the preflight transaction checks.
  * `preflightCommitment`(string, optional): Commitment level to use for preflight.&#x20;
    * Values: `finalised` `confirmed` `processed`
  * `maxRetries`(number, optional): Maximum number of times for the RPC node to retry sending the transaction to the leader.
  * `minContextSlot` (number, optional): Set the minimum slot at which to perform preflight transaction checks.

### Return Object

The method returns a base-58 encoded `string` value which is the first Transaction Signature embedded in the transaction. This is used to identify the transaction.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "sendTransaction",
  "params": [
    "4hXTCkRzt9WyecNzV1XPgCDfGAZzQKNxLXgynz5QDuWWPSAZBZSHptvWRL3BjCvzUXRdKvHL2b7yGrRQcWyaqsaBCncVG7BFggS8w9snUts67BSh3EqKpXLUm5UMHfD7ZBe9GhARjbNQMLJ1QD3Spr6oMTBU6EhdB4RD8CP2xUxr2u3d6fos36PD98XS6oX8TQjLpsMwncs5DAMiD4nNnR8NBfyghGCWvCVifVwvA8B8TJxE1aiyiv2L429BCWfyzAme5sZW8rDb14NeCQHhZbtNqfXhcp2tAnaAT"
  ]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": "2id3YC2jK9G5Wo2phDx4gJVAew8DcY5NAojnVuao8rkxwPYPe8cSwE5GzhEgJA2y8fVjDEo6iR6ykBvDxrTQrtpb",
  "id": 1
}
```
