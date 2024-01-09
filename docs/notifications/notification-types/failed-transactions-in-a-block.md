---
description: Stay Ahead of Failed Transactions with FAILED_TXS_PER_BLOCK Notifications
---

# Failed transactions in a block

In the fast-paced world of blockchain, keeping track of failed transactions is crucial for maintaining a secure and efficient platform. Tatum's OUTGOING\_FAILED\_TX notification type provides an invaluable tool to help you stay informed about all transactions in a block that fail to be included in a block.

### How to do it?

{% tabs %}
{% tab title="TypeScript / JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

(async () => {
    const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
    
    const subscription = await tatum.notification.subscribe.failedTxsPerBlock({
        url: 'https://<YOUR_WEBHOOK_URL>' // replace with your handler URL
    })
    console.log(`Now you will be notified about all failed transactions`)
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
    "type": "FAILED_TX_PER_BLOCK",
    "attr": {
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
  "amount": "0.001",
  "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
  "counterAddress": "0x690B9A9E9aa1C9dB991C7721a92d351Db4FaC990",
  "subscriptionType": "FAILED_TXS_PER_BLOCK"
  "blockNumber": 2913059,
  "txId": "0x062d236ccc044f68194a04008e98c3823271dc26160a4db9ae9303f9ecfc7bf6",
  "mempool": false
}
```
{% endcode %}

### Which blockchain networks are supported?

| Blockchain          | Mainnet                       | Testnet                                                    |
| ------------------- | ----------------------------- | ---------------------------------------------------------- |
| Ethereum            | Network.ETHEREUM              | <p>Network.ETHEREUM_SEPOLIA<br>Network.ETHEREUM_GOERLI</p> |
| Polygon             | Network.POLYGON               | Network.POLYGON\_MUMBAI                                    |
| Binance Smart Chain | Network.BINANCE\_SMART\_CHAIN | Network.BINANCE\_SMART\_CHAIN\_TESTNET                     |
| Celo                | Network.CELO                  | Network.CELO\_ALFAJORES                                    |
| Klaytn              | Network.KLAYTN                | Network.KLATN\_BAOBAB                                      |
| Solana              | Network.SOLANA                | Network.SOLANA\_DEVNET                                     |
| Tron                | Network.TRON                  | Network.TRON\_SHASTA                                       |

### Why Use FAILED\_TXS\_PER\_BLOCK Notifications?

FAILED\_TXS\_PER\_BLOCK notifications offer an effective way to monitor failed transactions in real-time. By focusing on transactions that fail to be included in a block, this notification type delivers several key benefits:

#### Real-time Monitoring

Stay informed about failed transactions as they occur. FAILED\_TXS\_PER\_BLOCK notifications provide real-time updates, allowing you to react promptly to important events and ensuring your application or platform always has the latest information.

#### Proactive Problem Solving

FAILED\_TXS\_PER\_BLOCK notifications help you identify and address the reasons behind failed transactions, such as insufficient gas fees, incorrect contract addresses, or network congestion. By proactively resolving these issues, you can minimize disruptions and maintain a smooth-running platform.

\
