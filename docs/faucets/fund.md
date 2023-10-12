---
description: >-
  This function allows you to request testnet tokens from faucet by passing in
  your address.
---

# Fund

## Overview

The Fund function within the Faucets submodule plays a pivotal role in obtaining testnet tokens for blockchain development, testing, and educational purposes. By simply passing the required parameters to this function, users can request testnet tokens from supported faucets seamlessly. This guide walks you through the process of utilizing the Fund function to bolster your blockchain projects.

## How to Fund a Wallet on a Supported Testnet

Utilise the TatumSDK (`@tatumio/tatum`) to fund a wallet on a supported testnet.

{% tabs %}
{% tab title="Typescript" %}
<pre class="language-typescript"><code class="lang-typescript"><a data-footnote-ref href="#user-content-fn-1">/</a>/ yarn add @tatumio/tatum

// Import necessary libraries from Tatum SDK
import { TatumSDK, Network, Ethereum } from '@tatumio/tatum'
<strong>
</strong>// Initialize the Tatum SDK for a specific blockchain network
// replace with your desired testnet
const tatum = await TatumSDK.init&#x3C;Ethereum>({
  network: Network.ETHEREUM_SEPOLIA,
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
</code></pre>
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

### Expected Response

#### Request Interface

```javascript
interface FaucetRequest {
    /**
     * The wallet address to fund.
     */
    address: string;
}
```

#### Response Interface

```javascript
interface ResponseDto<T> {
    /**
     * The actual payload of the response.
     */
    data: T;
    
    /**
     * The status of the response.
     */
    status: Status;
    
    /**
     * In case of ERROR status, this field contains the error message and a detailed description.
     */
    error?: ErrorWithMessage;
}
```

In this response interface, `data` will contain the transaction ID of the funding transaction, while `status` will indicate the success or failure of the request.

### Use Cases

* **Development and Testing:** Ensure a smooth development and testing process by funding your testnet wallet to test smart contracts, DApps, and other blockchain functionalities.
* **Education and Training:** Facilitate hands-on blockchain education by providing testnet tokens for students, educators, and workshop participants.
* **Hackathons:** Enable participants to hit the ground running in blockchain hackathons by providing a straightforward method to obtain testnet tokens.

### Summary

The Fund function in the Faucets submodule is a robust tool designed to streamline the process of obtaining testnet tokens. By leveraging this function, developers, educators, and blockchain enthusiasts can accelerate their projects and dive deeper into the blockchain ecosystem without any hurdles.

[^1]: 
