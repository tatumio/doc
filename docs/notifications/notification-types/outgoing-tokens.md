---
description: Stay on Top of Token Transactions with OUTGOING_FUNGIBLE_TX Notifications
---

# Outgoing Tokens

In the dynamic world of blockchain, staying updated with fungible token transactions is vital for maintaining a secure and efficient platform. Tatum's OUTGOING\_FUNGIBLE\_TX notification type offers a powerful solution to help you track outgoing fungible token transactions (e.g., ERC-20 / SPL transfers) from a specific address.

{% hint style="info" %}
A fungible token is a type of digital asset that is interchangeable and holds the same value across all its individual units. Examples of fungible tokens include popular cryptocurrencies like Bitcoin (BTC) and Ether (ETH), as well as ERC-20 tokens like Chainlink (LINK) and USD Coin (USDC), which can be easily exchanged, divided, and combined without altering their overall worth.
{% endhint %}

### How to do it?

{% tabs %}
{% tab title="TypeScript / JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

(async () => {
    const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
    
    const monitoredAddress = '0xF64E82131BE01618487Da5142fc9d289cbb60E9d'
    
    const subscription = await tatum.notification.subscribe.outgoingFungibleTx({
        address: monitoredAddress,
        url: 'https://<YOUR_WEBHOOK_URL>' // replace with your handler URL
    })
    console.log(`Now you will be notified about all outgoing token transactions on ${monitoredAddress}`)
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
    "type": "OUTGOING_FUNGIBLE_TX",
    "attr": {
      "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
      "chain": "ETH",
      "url": "https://&#x3C;YOUR_WEBHOOK_URL>"
    }
  }'
</code></pre>
{% endtab %}
{% endtabs %}

{% hint style="info" %}
This notification will be fired no matter what kind of Token leaves the monitored address.
{% endhint %}

### What does the fired webhook look like?

The fired notification webhook you will receive in your webhook listener will have the following format.

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "currency": "ETH",
  "chain": "ethereum-mainnet",
  "amount": "1",
  "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
  "counterAddress": "0x690B9A9E9aa1C9dB991C7721a92d351Db4FaC990",
  "subscriptionType": "OUTGOING_FUNGIBLE_TX",
  "blockNumber": 2913059,
  "txId": "0x062d236ccc044f68194a04008e98c3823271dc26160a4db9ae9303f9ecfc7bf6",
  "contractAddress": "0x743e8b6cc1676adae0e3243b5c011f7139c26128"
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
| Tezos               | Network.TEZOS                 | Network.TEZOS\_TESTNET                                     |
| Tron                | Network.TRON                  | Network.TRON\_SHASTA                                       |
