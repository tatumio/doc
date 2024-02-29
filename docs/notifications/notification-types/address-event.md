---
description: Unlock the Power of ADDRESS_EVENT Notifications for Real-Time Balance Updates
---

# Address event

Monitoring blockchain addresses can be a challenging and resource-intensive task, especially when you need to track balance updates across multiple token types and currencies. However, with Tatum's ADDRESS\_EVENT notification type, you can stay up-to-date with real-time balance updates, allowing you to streamline your operations and enhance the user experience.

### How to do it?

{% tabs %}
{% tab title="TypeScript / JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

(async () => {
    const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
    
    const monitoredAddress = '0xF64E82131BE01618487Da5142fc9d289cbb60E9d'
    
    const subscription = await tatum.notification.subscribe.addressEvent({
        address: monitoredAddress,
        url: 'https://<YOUR_WEBHOOK_URL>' // replace with your handler URL
    })
    console.log(`Now you will be notified about all ETH transactions on ${monitoredAddress}`)
})()
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>curl -i -X POST \
</strong>  https://api.tatum.io/v4/subscription?type=mainnet \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: &#x3C;YOUR-API-KEY>' \
  -d '{
    "type": "ADDRESS_EVENT",
    "attr": {
      "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
      "chain": "ETH",
      "url": "https://&#x3C;YOUR_WEBHOOK_URL>"
    }
  }'
</code></pre>
{% endtab %}
{% endtabs %}

### What does the fired webhook look like?

The fired notification webhook you will receive in your webhook listener will have the following format depends on case whether the address you subscribed on is sending or receiving address.\
\
**You subscribed sending address**

In this case you will get two notifications fired in your webhook listener:

1. Related to **`fee`** paid for transaction with defined `"type": "fee"`

```json
{
  "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
  "amount": "-0.000031500000168",
  "asset": "ETH",
  "blockNumber": 3553692,
  "txId": "0xde48b2572176eb3e1c4a2a9abe62c5552f778afcbba1ded8491a2ceb675a6390",
  "type": "fee",
  "chain": "ethereum-mainnet",
  "subscriptionType": "ADDRESS_EVENT"
}
```

2. Related to **`transaction`** itself with defined `"type": "native"` or "`fungible"` and etc.

{% code lineNumbers="true" %}
```json
{
  "address": "0xfAF0F447715dEeDF6Dd79c2fd1F7966F0CC647A1",
  "amount": "0.001",
  "asset": "ETH",
  "blockNumber": 3553692,
  "counterAddress": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
  "txId": "0xde48b2572176eb3e1c4a2a9abe62c5552f778afcbba1ded8491a2ceb675a6390",
  "type": "native",
  "chain": "ethereum-mainnet",
  "subscriptionType": "ADDRESS_EVENT"
}
```
{% endcode %}

**You subscribed receiving address**

In this case you will get only one single notification fired in your webhook listener:

```json
{
  "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
  "amount": "0.0001",
  "asset": "ETH",
  "blockNumber": 3553815,
  "counterAddress": "0xfAF0F447715dEeDF6Dd79c2fd1F7966F0CC647A1",
  "txId": "0x24e3c8d20449958b53186feb1844a022b864cba67bbca792330b5ab71035b499",
  "type": "native",
  "chain": "ethereum-mainnet",
  "subscriptionType": "ADDRESS_EVENT"
}
```

### Which blockchain networks are supported?

<table><thead><tr><th>Blockchain</th><th width="254.33333333333331">Mainnet</th><th>Testnet</th></tr></thead><tbody><tr><td>Ethereum</td><td>Network.ETHEREUM</td><td>Network.ETHEREUM_SEPOLIA, Network.ETHEREUM_GOERLI, Network.ETHEREUM_HOLESKY</td></tr><tr><td>Polygon</td><td>Network.POLYGON</td><td>Network.POLYGON_MUMBAI</td></tr><tr><td>Binance Smart Chain</td><td>Network.BINANCE_SMART_CHAIN</td><td>Network.BINANCE_SMART_CHAIN_TESTNET</td></tr><tr><td>Flare</td><td>Network.FLARE</td><td>Network.FLARE_COSTON, Network.FLARE_COSTON_2, Network.FLARE_SONGBIRD</td></tr><tr><td>Bitcoin</td><td>Network.BITCOIN</td><td>Network.BITCOIN_TESTNET</td></tr><tr><td>Litecoin</td><td>Network.LITECOIN</td><td>Network.LITECOIN_TESTNET</td></tr><tr><td>Dogecoin</td><td>Network.DOGECOIN</td><td>Network.DOGECOIN_TESTNET</td></tr><tr><td>Bitcoin Cash</td><td>Network.BITCOIN_CASH</td><td>Network.BITCOIN_CASH_TESTNET</td></tr><tr><td>Celo</td><td>Network.CELO</td><td>Network.CELO_ALFAJORES</td></tr><tr><td>Klaytn</td><td>Network.KLAYTN</td><td>Network.KLAYTN_BAOBAB</td></tr><tr><td>Solana</td><td>Network.SOLANA</td><td>Network.SOLANA_DEVNET</td></tr><tr><td>Tron</td><td>Network.TRON</td><td>Network.TRON_SHASTA</td></tr><tr><td>XRP</td><td>Network.XRP</td><td>Network.XRP_TESTNET</td></tr><tr><td>Tezos</td><td>Network.Tezos</td><td>Network.TEZOS_TESTNET</td></tr></tbody></table>

### Why Use ADDRESS\_EVENT Notifications?

The ADDRESS\_EVENT notification type delivers a webhook notification every time there is a balance update on a monitored address. This comprehensive notification system covers incoming and outgoing transactions for native currencies, as well as popular token standards like ERC-20, ERC-721, and ERC-1155. Moreover, it even tracks internal smart contract native transfers, ensuring a seamless monitoring experience across various blockchain activities.

Here are some key benefits of using ADDRESS\_EVENT notifications:

#### Real-time Monitoring

Stay informed about balance changes as they happen. ADDRESS\_EVENT notifications provide real-time updates, enabling you to react promptly to important events and ensuring that your application or platform always has the latest information.

#### Simplified Tracking

With support for native currencies, as well as popular token standards like ERC-20, ERC-721, and ERC-1155, ADDRESS\_EVENT notifications simplify the process of tracking balance changes across multiple token types. This feature allows you to focus on building functionality around these events, rather than spending time and resources on parsing raw blockchain data.

#### Enhanced Security

By receiving real-time notifications about balance changes, you can monitor your accounts or smart contracts for any suspicious activity. In case of unauthorized transactions or potential security risks, you can take immediate action to mitigate potential losses.

#### Improved User Experience

Integrating ADDRESS\_EVENT notifications into your application or platform keeps your users informed about balance updates, enhancing their experience and fostering trust in your service. Timely information empowers users to make informed decisions and interact confidently with your platform.
