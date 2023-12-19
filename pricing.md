---
description: Detailed pricing information about the Tatum Products
---

# 💵 Pricing

**As a developer you can start using Tatum for free,** [**register here**](https://dashboard.tatum.io) **to start using for free, and when you upgrade here's detailed information on the pricing of different products.**

## Products

Here's the list of things that your account gets charged for :

1. Sent Notifications: This is cost that you occur for every notification that is sent to you. Read more about the offering [here](docs/notifications/).
2. API Calls: This is the cost/per API call, and includes the following submodules:
   1. [NFTs Submodule](docs/nfts/)
   2. [Fungible Token](docs/fungible-tokens/)
   3. [Fee Estimation](docs/fee-estimation/)
   4. [Wallet Address Operations](docs/wallet-address-operations/)
   5. [Wallet Provider](docs/wallet-provider/)
   6. <mark style="background-color:orange;">v3</mark> [Blockchain Data API](https://apidoc.tatum.io/tag/Data-API)
   7. <mark style="background-color:orange;">v3</mark> [Blockchain Utility Calls](https://apidoc.tatum.io/tag/Algorand)
   8. <mark style="background-color:orange;">v3</mark> [Virtual Accounts](https://apidoc.tatum.io/tag/Account)
3. RPC Calls: This product includes the calls to full node functions in [RPC Submodule](docs/rpc/) and the [RPC Access via v3 product](https://apidoc.tatum.io/tag/Node-RPC), and is priced as cost/per RPC call.
4. Archive Calls: This product includes calls to the archive node in [RPC Submodule](docs/rpc/) and the [RPC Access via v3 product](https://apidoc.tatum.io/tag/Node-RPC), and is priced as cost/per RPC call.

<details>

<summary>Other v3 Products with gas costs**</summary>

1. <mark style="background-color:orange;">v3</mark> NFT Express: This feature allows you to mint NFTs on different chains,&#x20;
2. <mark style="background-color:orange;">v3</mark> Gas Pump: This feature allows you to pay gas fees for your or your user's operations in credits for v3, learn more about the feature [here](https://apidoc.tatum.io/tag/Gas-pump).
3. <mark style="background-color:orange;">v3</mark> Deployments: This feature allows you to deploy a smart contract. Read more about the feature [here](https://apidoc.tatum.com/#tag/Smart-Contract-interactions).
4. <mark style="background-color:orange;">v3</mark> Custodial Wallet: This feature allows you to create a custodial wallet and do transactions with it (requires gas cost). You can read more about the feature [here](https://apidoc.tatum.io/tag/Custodial-managed-wallets).

</details>

## Costs breakdown for the features&#x20;

> <mark style="background-color:green;">Before you assess pricing - full node RPC access via Tatum's v4 keys is half the cost of the industry standard and Archive RPC access is 2.5X lower that the standard.</mark>

<table><thead><tr><th width="178.5">Feature</th><th width="263">Flat Cost</th><th>Scaling Cost</th><th data-hidden>Cost</th></tr></thead><tbody><tr><td>Notifications</td><td>$0.00097 / sent notification</td><td>$0.00087 / sent notification</td><td>$0.00087 / sent notification</td></tr><tr><td>API Calls</td><td>$0.00000975 / sent call</td><td>$0.0000087 / sent call</td><td>$0.0000087 / call</td></tr><tr><td>RPC Calls</td><td>$0.00000975 / sent call</td><td>$0.0000087 / sent call</td><td>$0.0000087 / call</td></tr><tr><td>Archive Calls</td><td>$0.000195 / sent call</td><td>$0.000174 / sent call</td><td>$0.0000087 / call</td></tr><tr><td>v3 RPC Calls</td><td>$0.0000195 / sent call</td><td>$0.0000174 / sent call</td><td></td></tr><tr><td>v3 Archive Calls</td><td>$0.0004875 / sent call</td><td>$0.000435 / sent call</td><td></td></tr><tr><td>NFT Express, <br>Gas Pump, Deployments, Custodial Wallet,</td><td>$0.00000975 / sent call + gas**</td><td>$0.0000087 / sent call + gas**</td><td></td></tr></tbody></table>

**Note:** after $39 worth of usage we charge you the scaling cost for the specific product.

<mark style="background-color:yellow;">**Note:**</mark> <mark style="background-color:yellow;">**Cost + gas\*\***</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">means that you pay gas cost in dollars only when a specific function in the product requires a gas operation. To know more about those specific functions you can visit the product documentation page.</mark>

<mark style="background-color:yellow;">**Note:**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">If you haven't migrated your old API keys to the new v4 API keys, you can do that in your dashboard to lower your costs and access Tatum's new flexible</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**Pay As You Go pricing**</mark><mark style="background-color:yellow;">, extended features, usage analytics and more. Visit your</mark> [<mark style="background-color:yellow;">dashboard</mark>](https://dashboard.tatum.io) <mark style="background-color:yellow;">to migrate now.</mark>

## What's included in your Pay Go plan?

<details>

<summary>Case 1 : When you just use API calls and RPC Calls.</summary>

In this case you get 4 Million API calls.

</details>

<details>

<summary>Case 2 : When you use API calls, RPC Calls, and a v3 product with gas costs**</summary>

In this case you get 4 Million calls + you will be charged the gas cost in dollars, which you can track in the usage section in the [dashboard here](https://dashboard.tatum.io/usage).

</details>

<details>

<summary>Case 3 : What are the limitations of the free account?</summary>

The limits imposed on free accounts are as follows:

* 2 API Keys
* 3 Requests / sec on Full Nodes
* 2 Requests / min on Archive Nodes
* 100 Notifications / month
* 5 Subscriptions
* NFT Minting Express not available
* Analytics Dashboard limited&#x20;
* Debugging Tools limited
* Only Testnet Gas Coverage, Mainnet not available
* No Enterprise level support (Community Support still avaliable)

</details>

## FAQ

<details>

<summary>Are unused units of different products rolled over to next billing period.</summary>

Unused units in our Pay as you go plan don’t roll over to the next month.

</details>
