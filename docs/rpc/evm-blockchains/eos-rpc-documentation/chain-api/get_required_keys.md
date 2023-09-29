# get_required_keys

### Overview

The `get_required_keys` method returns the required keys that are needed to sign a transaction. This feature is extremely valuable for users and developers aiming to ensure secure and accurate transaction signatures, thus maintaining the integrity of transactions within the EOS blockchain.

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Eos>({ network: Network.EOS })

const response = await tatum.rpc.getRequiredKeys({
  transaction: { /* Transaction Object */ },
  available_keys: ["EOS..."]
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Example use cases:

1. **Secure Transaction Signing:**
   Users and developers can use the `get_required_keys` method to identify the specific keys required to sign a transaction, enhancing the security and accuracy of the signing process and avoiding unauthorized or faulty transactions.

2. **Blockchain Interaction:**
   This method is crucial for interactions and operations on the EOS blockchain where transactions are involved, ensuring that only the correct keys are utilized to sign the transactions, maintaining the validity and authenticity of the transactions.

3. **Smart Contract Interaction:**
   Developers interacting with smart contracts on the EOS blockchain can leverage this method to determine the appropriate keys to sign transactions related to smart contract execution, thereby maintaining the correctness and reliability of contract interactions.

### Request Parameters

The `get_required_keys` method necessitates the following parameters in the request body:

- `transaction` (object, required): The transaction object that needs to be signed.
- `availableKeys` (Array of strings, required): The array of available public keys.

### Return Object

The `get_required_keys` method typically returns an object containing the keys that are required to sign the transaction.

### JSON-RPC Request Example

```json
{
  "transaction": { /* Transaction Object */ },
  "available_keys": ["EOS..."]
}
```

## JSON-RPC Response Example

```json
{
  "required_keys": ["EOS..."]
}
```