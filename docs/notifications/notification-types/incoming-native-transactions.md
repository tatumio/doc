---
description: Stay on Top of Your Transactions with INCOMING_NATIVE_TX Notifications
---

# Incoming native transactions

In the world of blockchain, staying updated with incoming transactions is crucial for ensuring smooth operations and an optimal user experience. Tatum's INCOMING\_NATIVE\_TX notification type is designed to help you do just that – by sending webhook notifications every time there's an incoming native balance update on a monitored address.

### How to do it?

{% tabs %}
{% tab title="TypeScript / JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

(async () => {
    const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
    
    const monitoredAddress = '0xF64E82131BE01618487Da5142fc9d289cbb60E9d'
    
    const subscription = await tatum.notification.subscribe.incomingNativeTx({
        address: monitoredAddress,
        url: 'https://<YOUR_WEBHOOK_URL>' // replace with your handler URL
    })
    console.log(`Now you will be notified about all incoming ETH transactions on ${monitoredAddress}`)
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
    "type": "INCOMING_NATIVE_TX",
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
  "amount": "0.0001",
  "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
  "counterAddress": "0x0229338ee05154a406945899fb8c7bef36eb9220",
  "subscriptionType": "INCOMING_NATIVE_TX",
  "blockNumber": 3553920,
  "txId": "0x21c78973a2d47b1910d79b8586c55d13c732dfb41883ee5af4318dafc66a0db9",
  "mempool": false
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
| Bitcoin             | Network.BITCOIN               | Network.BITCOIN\_TESTNET                                                       |
| Litecoin            | Network.LITECOIN              | Network.LITECOIN\_TESTNET                                                      |
| Dogecoin            | Network.DOGECOIN              | Network.DOGECOIN\_TESTNET                                                      |
| Celo                | Network.CELO                  | Network.CELO\_ALFAJORES                                                        |
| Klaytn              | Network.KLAYTN                | Network.KLATN\_BAOBAB                                                          |
| Solana              | Network.SOLANA                | Network.SOLANA\_DEVNET                                                         |
| Tron                | Network.TRON                  | Network.TRON\_SHASTA                                                           |
| Tezos               | Network.TEZOS                 | Network.TEZOS\_TESTNET                                                         |
| XRP                 | Network.XRP                   | Network.XRP\_TESTNET                                                           |

