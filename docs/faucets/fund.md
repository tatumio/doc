---
description: >-
  This function allows you to request testnet tokens from faucet by passing in
  your address.
---

# Fund

## Overview

The Fund function within the Faucets submodule plays a pivotal role in obtaining testnet tokens for blockchain development, testing, and educational purposes. By simply passing the required parameters to this function, users can seamlessly request testnet tokens from supported faucets. By the end of this guide, you'll be ready to utilize the Fund function to bolster your blockchain projects.

## How to Fund a Wallet on a Supported Testnet

Utilise the TatumSDK (`@tatumio/tatum`) to fund a wallet on a supported testnet.

> <mark style="background-color:yellow;">Note : To use the function below for Sepolia Network, you would need to pass an api key. To find your current api key or to create a new one, head over to your</mark> [<mark style="background-color:yellow;">Dashboard</mark>](https://dashboard.tatum.io)<mark style="background-color:yellow;">.</mark>

{% tabs %}
{% tab title="Typescript" %}
```typescript
// yarn add @tatumio/tatum

// Import necessary libraries from Tatum SDK
import { TatumSDK, Network, Ethereum } from '@tatumio/tatum'

// Initialize the Tatum SDK for a specific blockchain network
// replace with your desired testnet
const tatum = await TatumSDK.init<Ethereum>({
  network: Network.ETHEREUM_SEPOLIA,
  apiKey: { v4: 'YOUR-API-KEY'}
})

// Define the parameters for the fund request
const res = await tatum.faucet.fund('0x712e3a792c974b3e3dbe41229ad4290791c75a82')

// Log the response to the console
if (res.data) {
  console.log(res.data)
} else {
  console.error(res.error)
}

// Destroy Tatum SDK - needed for stopping background jobs
await tatum.destroy()
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
// Install the Tatum SDK using yarn
// yarn add @tatumio/tatum

// Import necessary libraries from Tatum SDK
const { TatumSDK, Network } = require('@tatumio/tatum');

// Initialize the Tatum SDK for a specific blockchain network
// replace with your desired testnet
const tatum = await TatumSDK.init({
  network: Network.ETHEREUM_SEPOLIA,
  apiKey: { v4: 'YOUR-API-KEY'}
});

// Define the parameters for the fund request
const res = await tatum.faucet.fund('0x712e3a792c974b3e3dbe41229ad4290791c75a82');

// Log the response to the console
if (res.data) {
  console.log(res.data);
} else {
  console.error(res.error);
}

// Destroy Tatum SDK - needed for stopping background jobs
await tatum.destroy();

```
{% endtab %}
{% endtabs %}

<details>

<summary>Expected Response</summary>

```
{
  "data": {
    "txId": "0x9fe5af97d9279100a8442d9d10a7310c80ab3ed279568d3b08dae7c41d0d711a"
  },
  "status": "SUCCESS"
}
```

</details>

#### Parameters

<pre class="language-javascript"><code class="lang-javascript"><strong>// Address of the wallet you want the testnet token in
</strong><strong>address: string;
</strong></code></pre>

#### Response Interface

```typescript
interface ResponseDto<T> {
    /**
     * Actual payload of the response
     */
    data: T;
    /**
     * Status of the response
     */
    status: Status;
    /**
     * In case of ERROR status, this field contains the error message and detailed description
     */
    error?: ErrorWithMessage;
}

interface TxIdResponse {
    txId: string;
}
```

In this response interface, `data` will contain the transaction ID of the funding transaction, while `status` will indicate the success or failure of the request.

### Use Cases

* **Development and Testing:** Ensure a smooth development and testing process by funding your testnet wallet to test smart contracts, DApps, and other blockchain functionalities.
* **Education and Training:** Facilitate hands-on blockchain education by providing testnet tokens for students, educators, and workshop participants.
* **Hackathons:** Enable participants to hit the ground running in blockchain hackathons by providing a straightforward method to obtain testnet tokens.

### Summary

The Fund function in the Faucets submodule is a robust tool designed to streamline the process of obtaining testnet tokens. By leveraging this function, developers, educators, and blockchain enthusiasts can accelerate their projects and dive deeper into the blockchain ecosystem without any hurdles.
