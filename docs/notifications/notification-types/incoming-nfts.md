---
description: >-
  Stay Updated on Non-Fungible Token Transactions with INCOMING_NFT_TX
  Notifications
---

# Incoming NFTs

In the ever-expanding world of blockchain, keeping track of non-fungible token (NFT) transactions is crucial for maintaining a secure and efficient platform. Tatum's INCOMING\_NFT\_TX notification type offers a powerful solution to help you stay informed about incoming non-fungible token transactions (e.g., ERC-721 / SPL transfers) involving a specific address.

{% hint style="info" %}
A non-fungible token (NFT) is a unique digital asset that represents ownership of a one-of-a-kind item or piece of content, such as digital art, virtual real estate, or collectibles. Unlike fungible tokens, NFTs are not interchangeable and each NFT has a distinct value based on its rarity, provenance, and the demand for that specific token.

\
There are different NFT standards, most known are ERC-721 on EVM chains or SPL
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
    
    const subscription = await tatum.notification.subscribe.incomingNftTx({
        address: monitoredAddress,
        url: 'https://<YOUR_WEBHOOK_URL>' // replace with your handler URL
    })
    console.log(`Now you will be notified about all incoming NFT transactions on ${monitoredAddress}`)
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
    "type": "INCOMING_NFT_TX",
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
This notification will be fired no matter what kind of NFT is being transferred.
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
  "subscriptionType": "INCOMING_NFT_TX",
  "blockNumber": 110827114, 
  "txId": "0xe118976ba31815f81301341b4e211825bce1393cac1c4215075177b0a6b98930", 
  "contractAddress": "0x7d3dda0430471fe460c07b1ecab35670ef4ce85b", 
  "tokenId": "1450000023306",
  "metadataURI": "https://touhao.bj.bcebos.com/nft/metadata/1450000023306.json"
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
| Solana              | Network.SOLANA                | Network.SOLANA\_DEVNET                                                   |
| Tezos               | Network.TEZOS                 | Network.TEZOS\_TESTNET                                                   |
| Tron                | Network.TRON                  | Network.TRON\_SHASTA                                                     |
