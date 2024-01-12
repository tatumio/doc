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

| Blockchain          | Mainnet                       | Testnet                                                    |
| ------------------- | ----------------------------- | ---------------------------------------------------------- |
| Ethereum            | Network.ETHEREUM              | <p>Network.ETHEREUM_SEPOLIA<br>Network.ETHEREUM_GOERLI</p> |
| Polygon             | Network.POLYGON               | Network.POLYGON\_MUMBAI                                    |
| Binance Smart Chain | Network.BINANCE\_SMART\_CHAIN | Network.BINANCE\_SMART\_CHAIN\_TESTNET                     |
| Bitcoin             | Network.BITCOIN               | Network.BITCOIN\_TESTNET                                   |
| Litecoin            | Network.LITECOIN              | Network.LITECOIN\_TESTNET                                  |
| Dogecoin            | Network.DOGECOIN              | Network.DOGECOIN\_TESTNET                                  |
| Bitcoin Cash        | Network.BITCOIN\_CASH         | Network.BITCOIN\_CASH\_TESTNET                             |
| Celo                | Network.CELO                  | Network.CELO\_ALFAJORES                                    |
| Klaytn              | Network.KLAYTN                | Network.KLAYTN\_BAOBAB                                     |
| Solana              | Network.SOLANA                | Network.SOLANA\_DEVNET                                     |
| Tron                | Network.TRON                  | Network.TRON\_SHASTA                                       |
| XRP                 | Network.XRP                   | Network.XRP\_TESTNET                                       |
| Tezos               | Network.Tezos                 | Network.TEZOS\_TESTNET                                     |

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
