---
description: Master Your Outgoing Transactions with OUTGOING_NATIVE_TX Notifications
---

# Outgoing native transactions

Monitoring outgoing transactions is essential for maintaining a secure and efficient blockchain platform. Tatum's OUTGOING\_NATIVE\_TX notification type offers a powerful solution to help you stay informed about outgoing native balance updates on a monitored address, simplifying your operations and enhancing user experience.

### How to do it?

{% tabs %}
{% tab title="TypeScript / JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

(async () => {
    const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
    
    const monitoredAddress = '0xF64E82131BE01618487Da5142fc9d289cbb60E9d'
    
    const subscription = await tatum.notification.subscribe.outgoingNativeTx({
        address: monitoredAddress,
        url: 'https://<YOUR_WEBHOOK_URL>' // replace with your handler URL
    })
    console.log(`Now you will be notified about all outgoing ETH transactions on ${monitoredAddress}`)
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
    "type": "OUTGOING_NATIVE_TX",
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
  "amount": "0.001",
  "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
  "counterAddress": "0x690B9A9E9aa1C9dB991C7721a92d351Db4FaC990",
  "subscriptionType": "OUTGOING_NATIVE_TX",
  "blockNumber": 3553968,
  "txId": "0xac4b590e7668ca2adfd7cceef398d9859de23e61e1a46cfa9f79ac29a1ddc541",
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
| Bitcoin             | Network.BITCOIN               | Network.BITCOIN\_TESTNET                                   |
| Litecoin            | Network.LITECOIN              | Network.LITECOIN\_TESTNET                                  |
| Celo                | Network.CELO                  | Network.CELO\_ALFAJORES                                    |
| Klaytn              | Network.KLAYTN                | Network.KLATN\_BAOBAB                                      |
| Solana              | Network.SOLANA                | Network.SOLANA\_DEVNET                                     |
| Tron                | Network.TRON                  | Network.TRON\_SHASTA                                       |
| XRP                 | Network.XRP                   | Network.XRP\_TESTNET                                       |
