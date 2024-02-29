---
description: Stay Ahead of Failed Transactions with OUTGOING_FAILED_TX Notifications
---

# Outgoing failed transactions

In the fast-paced world of blockchain, keeping track of failed transactions is crucial for maintaining a secure and efficient platform. Tatum's OUTGOING\_FAILED\_TX notification type provides an invaluable tool to help you stay informed about transactions from monitored addresses that fail to be included in a block.

### How to do it?

{% tabs %}
{% tab title="TypeScript / JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

(async () => {
    const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
    
    const monitoredAddress = '0xF64E82131BE01618487Da5142fc9d289cbb60E9d'
    
    const subscription = await tatum.notification.subscribe.outgoingFailedTx({
        address: monitoredAddress,
        url: 'https://<YOUR_WEBHOOK_URL>' // replace with your handler URL
    })
    console.log(`Now you will be notified about all outgoing failed transactions on ${monitoredAddress}`)
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
    "type": "OUTGOING_FAILED_TX",
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

The fired notification webhook you will receive in your webhook listener will have the following format.

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
  "amount": "0.001",
  "blockNumber": 2913059,
  "counterAddress": "0x690B9A9E9aa1C9dB991C7721a92d351Db4FaC990",
  "txId": "0x062d236ccc044f68194a04008e98c3823271dc26160a4db9ae9303f9ecfc7bf6",
  "chain": "ethereum-mainnet",
  "subscriptionType": "OUTGOING_FAILED_TX",
  "currency": "ETH"
}
```
{% endcode %}

### Which blockchain networks are supported?

| Blockchain          | Mainnet                       | Testnet                                                                        |
| ------------------- | ----------------------------- | ------------------------------------------------------------------------------ |
| Ethereum            | Network.ETHEREUM              | Network.ETHEREUM\_SEPOLIA, Network.ETHEREUM\_GOERLI, Network.ETHEREUM\_HOLESKY |
| Polygon             | Network.POLYGON               | Network.POLYGON\_MUMBAI                                                        |
| Binance Smart Chain | Network.BINANCE\_SMART\_CHAIN | Network.BINANCE\_SMART\_CHAIN\_TESTNET                                         |
| Flare               | Network.FLARE                 | Network.FLARE\_COSTON, Network.FLARE\_COSTON\_2, Network.FLARE\_SONGBIRD       |
| Celo                | Network.CELO                  | Network.CELO\_ALFAJORES                                                        |
| Klaytn              | Network.KLAYTN                | Network.KLATN\_BAOBAB                                                          |
| Tezos               | Network.TEZOS                 | Network.TEZOS\_TESTNET                                                         |
| XRP                 | Network.XRP                   | <p>Network.XRP<br>Network.XRP_TESTNET</p>                                      |

### Why Use OUTGOING\_FAILED\_TX Notifications?

OUTGOING\_FAILED\_TX notifications offer an effective way to monitor failed transactions in real-time. By focusing on transactions that fail to be included in a block, this notification type delivers several key benefits:

#### Real-time Monitoring

Stay informed about failed transactions as they occur. OUTGOING\_FAILED\_TX notifications provide real-time updates, allowing you to react promptly to important events and ensuring your application or platform always has the latest information.

#### Proactive Problem Solving

OUTGOING\_FAILED\_TX notifications help you identify and address the reasons behind failed transactions, such as insufficient gas fees, incorrect contract addresses, or network congestion. By proactively resolving these issues, you can minimize disruptions and maintain a smooth-running platform.

\
