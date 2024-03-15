---
description: Stay Informed About Transaction Fees with PAID_FEE Notifications
---

# Paid fee

In the complex world of blockchain, keeping track of transaction fees is crucial for maintaining a transparent and efficient platform. Tatum's PAID\_FEE notification type provides a valuable tool to help you stay informed about fees paid as part of transactions involving a specific address.

### How to do it?

{% tabs %}
{% tab title="TypeScript / JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

(async () => {
    const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
    
    const monitoredAddress = '0xF64E82131BE01618487Da5142fc9d289cbb60E9d'
    
    const subscription = await tatum.notification.subscribe.paidFee({
        address: monitoredAddress,
        url: 'https://<YOUR_WEBHOOK_URL>' // replace with your handler URL
    })
    console.log(`Now you will be notified about all paid fees on ${monitoredAddress}`)
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
    "type": "PAID_FEE",
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
  "currency": "ETH",
  "chain": "ethereum-mainnet",
  "amount": "0.000031500000168",
  "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
  "subscriptionType": "PAID_FEE",
  "blockNumber": 2913059,
  "txId": "0x062d236ccc044f68194a04008e98c3823271dc26160a4db9ae9303f9ecfc7bf6",
  "mempool": false
}
```
{% endcode %}

### Which blockchain networks are supported?

| Blockchain          | Mainnet                       | Testnet                                                                  |
| ------------------- | ----------------------------- | ------------------------------------------------------------------------ |
| Ethereum            | Network.ETHEREUM              | Network.ETHEREUM\_SEPOLIA, Network.ETHEREUM\_HOLESKY                     |
| Polygon             | Network.POLYGON               | Network.POLYGON\_MUMBAI                                                  |
| Binance Smart Chain | Network.BINANCE\_SMART\_CHAIN | Network.BINANCE\_SMART\_CHAIN\_TESTNET                                   |
| Flare               | Network.FLARE                 | Network.FLARE\_COSTON, Network.FLARE\_COSTON\_2, Network.FLARE\_SONGBIRD |
| Celo                | Network.CELO                  | Network.CELO\_ALFAJORES                                                  |
| Klaytn              | Network.KLAYTN                | Network.KLATN\_BAOBAB                                                    |
| Cronos              | Network.CRONOS                | Network.CRONOS\_TESTNET                                                  |
| XRP                 | Network.XRP                   | Network.XRP\_TESTNET                                                     |
| Tezos               | Network.Tezos                 | Network.TEZOS\_TESTNET                                                   |
| Tron                | Network.TRON                  | Network.TRON\_SHASTA                                                     |

### Why Use PAID\_FEE Notifications?

PAID\_FEE notifications offer an effective way to monitor transaction fees in real-time. By focusing on fees paid in transactions involving a specific address, this notification type delivers several key benefits:

#### Real-time Monitoring

Stay informed about transaction fees as they occur. PAID\_FEE notifications provide real-time updates, allowing you to react promptly to important events and ensuring your application or platform always has the latest information.

#### Enhanced Transparency

Receiving real-time notifications about transaction fees helps you maintain a transparent and accountable platform. Users can clearly see the fees associated with their transactions, fostering trust in your service and promoting a fair ecosystem.

#### Proactive Fee Management

PAID\_FEE notifications help you identify and address potential issues related to transaction fees, such as underpayment or overpayment. By proactively resolving these issues, you can minimize disruptions and maintain a smooth-running platform.
