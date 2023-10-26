---
description: >-
  This function fetches real-time gas fee data, including slow, medium, and fast
  fees, based on the most recent recalculation, providing transparency for
  blockchain transaction cost estimation.
---

# getCurrentFee

## Overview

The `getCurrentFee()` function is a method provided by the Tatum Fee Submodule in the Tatum SDK. It enables developers to fetch the current gas fee for a specific blockchain network. This function facilitates access to real-time fee information, allowing users to make informed decisions about transaction costs and optimize their blockchain interactions.

#### Syntax

```javascript
const fee = await tatum.fee.getCurrentFee();
```

#### Note

<mark style="background-color:yellow;">This function currently works with the previous version of our api & requires an explicit version initialisation for the main object to be called.</mark>

```javascript
// Some code
const tatum = await TatumSDK.init(
{ network: Network.ETHEREUM, version: ApiVersion.V3 }
);
```

## Codepen

{% embed url="https://codepen.io/tatum-devrel/pen/abQPQoz" %}

## Response DTO

```typescript
interface CurrentEvmFee {
  /* Chain for the Response */
  chain: Network
  
  /* gasPrice for slow, medium, fast, baseFee & unit */
  gasPrice: {
    slow: string
    medium: string
    fast: string
    baseFee: string
    unit: string
  }
  
  /* Last time when the gas fees was Recalculated */
  lastRecalculated: string

  /* This property specifies the block number or block 
  identifier on the blockchain network on which the current
  gas fee data is based. */
  basedOnBlockNumber: string
}
```

#### Return Value

The `getCurrentFee()` function returns a Promise that resolves to an object containing the current gas fee data for the selected network. The specific structure of the returned object may vary depending on the blockchain network and API version being used.

#### Usage

1. Initialise the Tatum SDK with the desired network and API version using `TatumSDK.init()`.

```javascript
const tatum = await TatumSDK.init({ network: Network.ETHEREUM, version: ApiVersion.V3 });
```

2. Call the `getCurrentFee()` function to fetch the current gas fee for the selected network.

```javascript
const fee = await tatum.fee.getCurrentFee();
```

3. Access the fee data returned by the function to retrieve the gas fee information.

```javascript
console.log(fee.data.gasPrice.fast); // Display the fast gas fee
```

## Supported blockchains

* ETHEREUM&#x20;
* BITCOIN&#x20;
* LITECOIN&#x20;
* DOGECOIN&#x20;

## Example

The following example demonstrates the usage of the `getCurrentFee()` function within an event listener:

```javascript
const button = document.getElementById("fetch-fee");
const feeContainer = document.getElementById("fee-container");

button.addEventListener("click", async () => {
  const tatum = await TatumSDK.init({ network: Network.ETHEREUM, version: ApiVersion.V3 });

  const fee = await tatum.fee.getCurrentFee();

  feeContainer.textContent = `Current Fee: ${fee.data.gasPrice.fast}`;
});
```

In this example, when the "Fetch Fee" button is clicked, the `getCurrentFee()` function is called to fetch the current gas fee for the Ethereum network. The returned fee data is then used to update the content of the `feeContainer` element with the fast gas fee value.

Note: The example assumes that the HTML structure and event listeners are properly set up as described in the previous sections. Adjust the code according to your specific requirements and chosen blockchain network.
