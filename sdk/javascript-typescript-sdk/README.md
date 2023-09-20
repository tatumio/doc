---
description: >-
  Tatum offers a very powerful JS/TS SDK which can help developers to make dapps
  easier and quicker.
---

# JavaScript / TypeScript SDK

This page provides a step-by-step guide on getting started creating a dapp that fetches the native balance of a user under a minute.

## Prerequisites

Before diving into TatumSDK, ensure that you have the following prerequisites installed:

* **Node.js**: Ensure you have the latest LTS version installed.
* **npm**: npm is bundled with Node.js, so installing Node.js should automatically install npm.

## Installation

To install TatumSDK, simply run the following command in your terminal or command prompt:

#### Install using [npm](https://www.npmjs.com/)

{% code lineNumbers="true" %}
```bash
npm install @tatumio/tatum
```
{% endcode %}

#### Install using [yarn](https://yarnpkg.com/)

{% code overflow="wrap" lineNumbers="true" %}
```bash
yarn add @tatumio/tatum
```
{% endcode %}

#### Install using [pnpm](https://pnpm.io/)

{% code lineNumbers="true" %}
```bash
pnpm install @tatumio/tatum
```
{% endcode %}

## Making your first Call

Now that you have installed Tatum SDk, lets make your first call in which we will fetch the native balance of wallet in just 3 steps.

Here's the code snippet for same,

```javascript
import { TatumSDK, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init({ network: Network.ETHEREUM });
const balance = await tatum.address.getBalance({
    addresses: [addressInput.value],
});
console.log(balance.data[0]);
});
```

Try the first call in the codepen below.

{% embed url="https://codepen.io/tatum-devrel/pen/MWzZXqz" %}
Make your first call.
{% endembed %}

Interesting? You can follow this full [Get Started guide ](../get-started-with-tatum-sdk.md)to start building your own dapps.
