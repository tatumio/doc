# eth_getTransactionCount

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Base, Network } from "@tatumio/tatum";

const tatum = await TatumSDK.init<Base>({ network: Network.BASE });

const result = await tatum.rpc.getTransactionCount(
  "0xE75C6D867f658E534450e0595dD0eb4FCc7a4060",
  "latest"
);

await tatum.destroy(); // Destroy Tatum SDK - needed for stopping background jobs
```

{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_getTransactionCount` method retrieves the number of transactions sent from a given address. It is a useful method for developers who need to keep track of an account's nonce value to avoid transaction collisions or incorrect order of execution. The nonce value is essential for ensuring transaction uniqueness and preventing replay attacks.

Use cases for this method include:

- Determining the nonce value for a new transaction to be sent from a specific address
- Monitoring the number of transactions sent by an address to observe its activity
- Troubleshooting transaction issues and verifying if a transaction was submitted successfully

### Parameters

The `eth_getTransactionCount` method accepts two parameters:

1. **`address`** - The address whose transaction count will be retrieved.
   - Example: `"0xE75C6D867f658E534450e0595dD0eb4FCc7a4060"`
2. **`blockParameter`** - A string indicating the block number or block state to consider when retrieving the transaction count.
   - Possible values: `"earliest"`, `"latest"`, `"pending"`, or a specific block number in hexadecimal format
   - Example: `"latest"`

### Return Object

The method returns a single value:

- **`transactionCount`** - A hexadecimal representation of the number of transactions sent from the specified address.
  - Example: `"0x1e"`

#### Response:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x1e"
}
```
