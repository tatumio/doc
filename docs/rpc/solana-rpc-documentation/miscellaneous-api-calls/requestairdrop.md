# requestAirdrop

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum
import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({network: Network.SOLANA_DEVNET})

const res = await tatum.rpc.requestAirdrop('G35uLP74uj4eCSfMs17ePKtK1ThuH8JKebAP1T2y6CYw',1000000000)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `requestAirdrop` method is used to request an airdrop of lamports to a specific Pubkey. This is particularly useful for testing or development environments where you need to distribute tokens for various accounts for testing purposes.

### Parameters

* `pubkey` (string, required): The public key of the account that will receive the lamports, represented as a base-58 encoded string.
* `lamports` (integer, required): The number of lamports to airdrop.

### Return Object

The result is a string representing the transaction signature of the airdrop, as a base-58 encoded string.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0", 
  "id": 1,
  "method": "requestAirdrop",
  "params": [
    "G35uLP74uj4eCSfMs17ePKtK1ThuH8JKebAP1T2y6CYw",
    1000000000
  ]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": "5VERv8NMvzbJMEkV8xnrLkEaWRtSz9CosKDYjCJjBRnbJLgp8uirBgmQpjKhoR4tjF3ZpRzrFmBV6UjKdiSZkQUW",
  "id": 1
}
```
