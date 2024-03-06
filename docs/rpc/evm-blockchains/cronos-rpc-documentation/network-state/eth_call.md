# eth\_call

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const result = await tatum.rpc.call({
  "to": "0xc21223249CA28397B4B6541dfFaEcC539BfF0c59", // Replace with the ERC-20 token contract address
  "data": "0x70a082310000000000000000000000008c9ac9e60e96db6b0da7ca9b8d06e0572fc289d6" // The function signature for balanceOf(address), followed by the address 
}, "latest")

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

Executes a new message call immediately without creating a transaction on the block chain. Often used for executing read-only smart contract functions, for example the `balanceOf` for an ERC-20 contract.

Top 5 most commonly used use cases for `eth_call`:

1. **Retrieve Token Balance:** Check an ERC-20 token balance for an address.
2. **Query Contract State:** Get contract data, like a game score or auction status.
3. **Validate Inputs:** Pre-validate function inputs before sending a transaction.
4. **Price Oracles:** Fetch real-time price data for decentralized applications.
5. **Gas Estimation:** Estimate gas costs for future transactions.

### **Parameters**

1. `Object` - The transaction call object

* `from`: `DATA`, 20 Bytes - (optional) The address the transaction is sent from.
* `to`: `DATA`, 20 Bytes - The address the transaction is directed to.
* `gas`: `QUANTITY` - (optional) Integer of the gas provided for the transaction execution. eth\_call consumes zero gas, but this parameter may be needed by some executions.
* `gasPrice`: `QUANTITY` - (optional) Integer of the gasPrice used for each paid gas
* `value`: `QUANTITY` - (optional) Integer of the value sent with this transaction
* `data`: `DATA` - (optional) Hash of the method signature and encoded parameters. For details see [Ethereum Contract ABI in the Solidity documentation(opens in a new tab)](https://docs.soliditylang.org/en/latest/abi-spec.html)

2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`

### Return Object

`DATA` - the return value of executed contract.