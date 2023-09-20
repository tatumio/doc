---
description: >-
  In this page we will be comparing the most popular SDK's and the factors which
  you as a developer should consider for building your next big web3 project.
---

# Selecting the best SDK

## TLDR;

We have done a full comparison of most of the popular SDK's out there, on the parameters in the categories **Feature Set,** **Chain Support,** **Ease of Use, Performance & Composability** , & **Robustness.** You can find all the [full comparison here.](full-comparison.md)

In Short here's we are the coolest **😎**, But here's why you shouldn't use us.

1. We don't support all new random EVM chains, Though the major ones and you can [find all we support here](../../docs/notifications/supported-types-and-blockchain-networks.md) & if this is a deal breaker then third-web, Ethers or Web3.js might be best for your needs.

But wait here's **what you would lose**.

1. **Performance benefits** due to less dependencies
2. Most reliable RPC access straight from SDK with **Provider Agnosticism**.
3. Most **Simple Integration & Use**, with Better **SDK Composability** & the best product Documentation.
4. **UTXO Support & Chain Agnostic Response/Response Abstraction.**

## Why use a web3 SDK?

If you are here, you probably have made your mind to use something like Tatum SDK, but if you are still thinking on why its better to use Tatum SDK over any other RPC service or the generic api provider's, here are some of the reasons why you might choose a Web3 SDK over RPCs and generic APIs:

1. **Ease of Use:** Web3 SDKs provide high-level abstractions for interacting with the blockchain. They simplify many complex tasks involved in interacting with the blockchain, such as transaction signing, data encoding/decoding, and contract interaction, thereby reducing the learning curve and development time.
2. **Feature Set:** SDK's can provide a much more generous feature sets tailored to use cases like one single function call to get all the different types of token balances for your portfolio dapp.
3. **One Stop Shop:** Some cool SDK's like ours can help you get NFT functionalities, Tokens, Notifications, Wallet Connect & even RPC access for your contract management all packed in one. (Yet being the smallest and least dependent one).
4. **Response Abstraction:** Working with default RPC functions can be tricky due to their raw responses and specially in a cross chain environment. Thus having Response Abstraction or more human specific response can be of a great help.\
   Eg: Fetching token balances gives you value in decimals numbers with information like symbol, & total decimal places etc. instead of just big Numbers.

## Other crucial factors in decision

We already know some must have's you should look for in an SDK, but here's equally more important aspects if not more.

1. **Performance benefits:** This is one of the most crucial for a lot of developers, the impact of the sdk on the environment, which basically is due to the size of SDK & the number of dependencies it has. The lower the number for both of this factors the better it is.
2. **Provider Agnosticism:** Another crucial check which ensures you will have a friction less development journey is "_Provider Agnosticism_" which basically means you get more options to choose your base feature provider which will be RPC in this case. Whereas otherwise you will be locked to a single provider even when they are down.
3. **Simple Integration & Use:** Product documentation is an always overlooked but yet plays a crucial role while you are developing applications with sdk's, imagine having guests at house and you have to cook something for them and all your recipe book is jumbled and tough to go through.
4. **SDK Composability:** How an sdk in composed in terms of hierarchy matters, for example if i tell you that `tatum.nft.getBalance()` gets you all the nft balances can you guess what would be the call for fetching all token balances? And not just a better SDK architecture but the ability to contribute it to shape it the way you like matters as well.

## **Conclusion:**

Tired at this point I could have just told you to use Tatum SDK and that's the best way, but I will still share this unbiased comparison blog to let you decide on your own & if you disagree to any of it or have any more factors we should consider, create a proposal here and we shall get it moving.
