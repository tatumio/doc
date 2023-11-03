# Simulate Transfer Erc20

## Overview

The `simulateTransferErc20` function within the Transaction Simulator extension is instrumental for simulating ERC20 token transfers on EVM-based blockchains. This function allows developers to comprehend and test the behavior of ERC20 token transfers without interacting with the live blockchain. This guide delineates the steps to utilize the `simulateTransferErc20` function to enrich your blockchain projects.

## How to Simulate an ERC20 Transfer

Utilize the provided library to simulate an ERC20 transfer on an EVM-based blockchain.

{% tabs %}
{% tab title="Typescript" %}
<pre class="language-typescript"><code class="lang-typescript">// Import necessary libraries
<strong>import { TatumSDK, Network, Ethereum } from '@tatumio/tatum';
</strong>import { TransactionSimulator } from '@tatumio/transaction-simulator';

// Initialize the SDK for a specific blockchain network
const tatumSdk = await TatumSDK.init&#x3C;Ethereum>({
     network: Network.ETHEREUM,
     configureExtensions: [
         TransactionSimulator,
     ]
 })

// Define Your Payload
const tokenTransferPayload: TokenTransfer = {
  to: 'recipient_address',
  from: 'sender_address',
  gas: '0xB411', // optional
  gasPrice: '0x4B16C370A', //optional
  value: 500, // example token amount to send
  tokenContractAddress: 'your_erc20_token_contract_address'
};

// Call simulateTransferErc20
const tokenSimulationResult = await await tatumSdk.extension(TransactionSimulator)
.simulateTransferErc20(tokenTransferPayload);

// Check simulation results
console.log(tokenSimulationResult);
</code></pre>
{% endtab %}

{% tab title="Javascript" %}
```javascript
// Import necessary libraries
import { TatumSDK, Network, Ethereum } from '@tatumio/tatum';
import { simulateTransferErc20, Erc20Transfer } from '@tatumio/transaction-simulator';

// Initialize the SDK for a specific blockchain network
const tatumSdk = await TatumSDK.init<Ethereum>({
     network: Network.ETHEREUM,
     configureExtensions: [
         TransactionSimulator,
     ]
 })

// Define Your Payload
const tokenTransferPayload: TokenTransfer = {
  to: 'recipient_address',
  from: 'sender_address',
  gas: '0xB411', // optional
  gasPrice: '0x4B16C370A', //optional
  value: 500, // example token amount to send
  tokenContractAddress: 'your_erc20_token_contract_address'
};

// Call simulateTransferErc20
const tokenSimulationResult = await simulateTransferErc20(tokenTransferPayload);

// Check simulation results
console.log(tokenSimulationResult);
```
{% endtab %}
{% endtabs %}

### Parameters

* `to`: Address of the recipient.
* `from`: Address of the sender.
* `gas`: (Optional) Gas limit for the transaction.
* `gasPrice`: (Optional) Gas price for the transaction.
* `value`: Amount to send in wei.
* tokenContractAddress : Token address you want to interact with.

<details>

<summary>Expected Response</summary>

```json5
{
  "transactionDetails": {
    "from": "0xDce92f40cAdDE2C4e3EA78b8892c540e6bFe2f81",
    "to": "0xaf758da9f7bdaa7590175193388e9c99427cc2d2",
    "tokenContractAddress": "0xdac17f958d2ee523a2206206994597c13d831ec7",
    "data": "0xa9059cbb000000000000000000000000af758da9f7bdaa7590175193388e9c99427cc2d2000000000000000000000000000000000000000000000000000000001908b100",
    "gasLimit": 46097,
    "gasPrice": 20156528394
  },
  "status": "success",
  "balanceChanges": {
    "0xDce92f40cAdDE2C4e3EA78b8892c540e6bFe2f81": {
      "from": 243656557299636170000,
      "to": 243655628144146780000
    }
  },
  "tokenTransfers": {
    "0xdac17f958d2ee523a2206206994597c13d831ec7": {
      "name": "TetherUSD",
      "symbol": "USDT",
      "decimals": 6,
      "0xDce92f40cAdDE2C4e3EA78b8892c540e6bFe2f81": {
        "from": 2387468.080258,
        "to": 2387048.080258
      },
      "0xaf758da9f7bdaa7590175193388e9c99427cc2d2": {
        "from": 422.304,
        "to": 842.304
      }
    }
  }
}
```

</details>

### Use Cases

* **Development and Testing:** Simulate ERC20 transactions to test smart contracts, DApps, and other blockchain functionalities in a risk-free environment.
* **Education and Training:** Foster practical blockchain education by simulating real-world ERC20 transaction scenarios.
* **Hackathons:** Empower participants to grasp the implications of ERC20 transactions without the necessity of a live blockchain.

### Summary

The `simulateTransferErc20` function in the Transaction Simulator submodule is a robust tool intended to provide a simulated environment for understanding and testing ERC20 token transfers on EVM-based blockchains. Utilising this function will enable developers, educators, and blockchain enthusiasts to bolster their understanding and expedite their projects within the blockchain ecosystem.

\
