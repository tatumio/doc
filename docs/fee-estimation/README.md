---
description: >-
  The Fee submodule is a part of the Tatum SDK, which allows developers to
  interact with various blockchain networks. It specifically provides
  functionalities related to retrieving gas fees.
---

# ⛽ Fee Estimation

## Introduction

The Tatum Fee Submodule is a component of the Tatum SDK that provides a simple way to fetch and display the current gas fee for a specific blockchain network. Gas fees are a vital aspect of blockchain transactions, representing the cost required to execute operations on the network. By utilising this submodule, developers can easily retrieve and showcase the current gas fee for various blockchain networks, enabling better transparency and user experience within decentralised applications.

## Get Started

```javascript
import { TatumSDK, Network, ApiVersion } from "@tatumio/tatum";

// Initialize the Tatum SDK with the desired network and API version
const tatum = await TatumSDK.init({ network: Network.ETHEREUM, version: ApiVersion.V1 });

// Fetch the current gas fee
const fee = await tatum.fee.getCurrentFee();

// Display the fetched fee in console
console.log(fee.data.gasPrice.fast);
});

```

## Use Cases

The Tatum Fee Submodule offers several use cases for developers working with blockchain networks. Some potential applications include:

#### Transaction Cost Estimation

Before executing a transaction on a blockchain network, it is essential to estimate the associated gas fee accurately. The Tatum Fee Submodule enables developers to fetch the current fee and use it to calculate the approximate transaction cost. This information allows users to make informed decisions and optimize their transaction parameters accordingly.

#### User-Friendly Fee Display

Displaying the current gas fee to end-users within a decentralised application can enhance their understanding of the transaction's cost. The Tatum Fee Submodule simplifies the process of fetching the fee and presenting it in a user-friendly format. Developers can integrate this functionality into their applications to show real-time gas fee updates, increasing transparency and facilitating user engagement.

#### Gas Fee Comparison

Comparing gas fees across different blockchain networks is crucial for users seeking the most cost-effective and efficient options. By utilising the Tatum Fee Submodule, developers can fetch and display fees from various supported networks simultaneously. This feature empowers users to evaluate and select networks based on current gas fees, enhancing the overall user experience.

## Why it's tough to know Gas fees at a point of time

Determining the precise gas fees at a particular moment can be challenging in the blockchain ecosystem due to several reasons:

#### Dynamic Fee Market

Blockchain networks often employ dynamic fee markets where fees fluctuate based on network congestion and demand. Gas fees are determined by a bidding process, where users compete to have their transactions included in the next block. As a result, gas fees can vary significantly within short timeframes, making it difficult to pinpoint the exact fee at any given point.

#### Lack of Standardisation

Different blockchain networks utilise varying fee models and calculation methods, further complicating the process of finding gas fees. Each network may have its own unit of measurement, fee structures, and mechanisms for determining transaction costs. This lack of standardisation makes it challenging to provide a unified approach to fetch gas fees across multiple networks.

#### Network-Specific Implementations

Fetching gas fees requires interacting with blockchain networks directly through their respective APIs or nodes. Each network may have its own specific implementation for retrieving fee data, including authentication requirements, rate limits, and API endpoints. Navigating these network-specific intricacies can be time-consuming and technically demanding for developers.

The Tatum Fee Submodule addresses these challenges by providing a simplified and standardised interface to fetch gas fees from supported networks, allowing developers to focus on integrating fee-related functionalities into their applications without dealing with the complexities of individual networks.

Note: The code provided in the initial question demonstrates a basic usage example of the Tatum Fee Submodule for fetching and displaying the current gas fee on the Ethereum network.
