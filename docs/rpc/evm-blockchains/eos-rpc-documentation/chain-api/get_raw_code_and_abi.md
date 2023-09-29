# get_raw_code_and_abi

### Overview

The `get_raw_code_and_abi` method is used to retrieve both the raw code and the ABI (Application Binary Interface) for a contract, based on the account name. This is pivotal for developers who wish to interact with, decode, and understand the underlying code and interfaces of smart contracts deployed on the EOS blockchain.

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Eos>({ network: Network.EOS })

const response = await tatum.rpc.getRawCodeAndAbi('eosio')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Example use cases:

1. **Understanding Smart Contracts:**
   Developers can use the `get_raw_code_and_abi` method to gain insights into the raw code and ABI of smart contracts, enabling them to understand and interact with the contract's methods, state variables, and structures more effectively.

2. **Development and Debugging:**
   This method is crucial for developers in the development and debugging phases, allowing for precise interaction and validation of the contract's code and interfaces, thereby facilitating a smoother development process.

3. **Enhanced Interaction with Smart Contracts:**
   With the detailed insight provided by this method, developers can optimize their interaction with the smart contracts, making the development of decentralized applications more efficient and robust.

### Request Parameters

The `get_raw_code_and_abi` method requires the following parameter in the request body:

- `accountName` (string, required): This can be `NamePrivileged`, `NameBasic`, `NameBid`, or `NameCatchAll`. It represents the name of the account for which the raw code and ABI are being requested.

### Return Object

Upon a successful request, the method returns an object containing the following details:

- `account_name` (string): Name of the account.
- `wasm` (string): The base64 encoded WebAssembly (WASM) code of the smart contract.
- `abi` (string): The base64 encoded ABI of the smart contract.

### JSON-RPC Request Example

```json
{
  "account_name": "eosio"
}
```
### JSON-RPC Response Example

```json
{
  "account_name": "eosio",
  "wasm": "base64EncodedWASM",
  "abi": "base64EncodedABI"
}
```