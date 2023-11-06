---
description: >-
  This function helps you to simulate a native transfer by passing a payload to
  the function simulateTransfer of the extension
  '@tatumio/transaction-simulator';
---

# Simulate Transfer

## Overview

The `simulateTransfer` function within the `Transaction Simulator` submodule serves a vital role in simulating native and ERC20 token transfers on EVM-based blockchains. This function is crucial for developers to test and understand the behavior of token transfers without interacting with the live blockchain. This guide provides a step-by-step approach to utilize the `simulateTransfer` function to enhance your blockchain projects.

## How to Simulate a Transfer

Utilize the provided library to simulate a transfer on an EVM-based blockchain.

{% tabs %}
{% tab title="Typescript" %}
<pre class="language-typescript"><code class="lang-typescript">// Import necessary libraries
<strong>import { TatumSDK, Network, Ethereum } from '@tatumio/tatum';
</strong>import { TransactionSimulator } from '@tatumio/transaction-simulator';

const tatumSdk = await TatumSDK.init&#x3C;Ethereum>({
     network: Network.ETHEREUM,
     configureExtensions: [
         TransactionSimulator,
     ]
 })
 
// Define Your Payload
const transferPayload: Transfer = {
  to: '0x0Ae9E7437092BB7E7Bd6Eccf0eF1ad05591f5B47',
  from: '0xDce92f40cAdDE2C4e3EA78b8892c540e6bFe2f81',
  gas: '0x5208',  // optional
  gasPrice: '0x4BA1C7B8C',  //optional
  value: 1000,  // example amount to send in wei
};

// Call simulateTransfer
const simulationResult = await tatumSdk.extension(TransactionSimulator)
.simulateTransfer(transferPayload);


// Check simulation results
console.log(simulationResult);
</code></pre>
{% endtab %}

{% tab title="Javascript" %}
```javascript
// Import necessary libraries
import { TatumSDK, Network } from '@tatumio/tatum';
import { simulateTransfer, Transfer } from '@tatumio/transaction-simulator';

const tatumSdk = await TatumSDK.init({
     network: Network.ETHEREUM,
     configureExtensions: [
         TransactionSimulator,
     ]
 })
 
// Define Your Payload
const transferPayload: Transfer = {
  to: '0x0Ae9E7437092BB7E7Bd6Eccf0eF1ad05591f5B47',
  from: '0xDce92f40cAdDE2C4e3EA78b8892c540e6bFe2f81',
  gas: '0x5208',  // optional
  gasPrice: '0x4BA1C7B8C',  //optional
  value: 1000,  // example amount to send in wei
};

// Call simulateTransfer
const simulationResult = await simulateTransfer(transferPayload);

// Check simulation results
console.log(simulationResult);
```
{% endtab %}
{% endtabs %}

### Parameters

* `to`: Address of the recipient.
* `from`: Address of the sender.
* `gas`: (Optional) Gas limit for the transaction.
* `gasPrice`: (Optional) Gas price for the transaction.
* `value`: Amount to send in wei.

<details>

<summary>Expected Response</summary>

```json5
{
  "transactionDetails": {
    "from": "0xDce92f40cAdDE2C4e3EA78b8892c540e6bFe2f81",
    "to": "0x0Ae9E7437092BB7E7Bd6Eccf0eF1ad05591f5B47",
    "value": 10000,
    "gasLimit": 21000,
    "gasPrice": 20302297996
  },
  "status": "success",
  "balanceChanges": {
    "0xDce92f40cAdDE2C4e3EA78b8892c540e6bFe2f81": {
      "from": 243323659206289750000,
      "to": 243323232858031850000
    },
    "0x0Ae9E7437092BB7E7Bd6Eccf0eF1ad05591f5B47": {
      "from": 8951104779026672,
      "to": 8951104779036672
    }
  }
}
```

</details>

### Response Interface

In this response interface, `transactionDetails` contains the details of the simulated transaction, `status` indicates the success or failure, and `balanceChanges` shows the balance changes for the involved addresses.

### Use Cases

* **Development and Testing:** Simulate transactions to test smart contracts, DApps, and other blockchain functionalities in a safe and controlled environment.
* **Education and Training:** Enhance hands-on blockchain education by simulating real-world transaction scenarios.
* **Hackathons:** Enable participants to understand the implications of transactions without the necessity of a live blockchain.

### Summary

The `simulateTransfer` function in the `Transaction Simulator` submodule is a powerful tool designed to provide a simulated environment for understanding and testing token transfers on EVM-based blockchains. Leveraging this function will enable developers, educators, and blockchain enthusiasts to enhance their understanding and expedite their projects in the blockchain ecosystem.
