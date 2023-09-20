---
description: Unleashing the Power of CONTRACT_ADDRESS_LOG_EVENT Notifications
---

# Contract Address Log Event

The world of blockchain and smart contracts is evolving at an unprecedented pace. CONTRACT\_ADDRESS\_LOG\_EVENT notifications offer a powerful way to stay informed about specific smart contract events in real-time. By utilizing this feature, you can enhance security, streamline data analysis, improve user experience, and maintain flexibility in your monitoring approach. If you're a developer or business involved in the blockchain space, it's time to harness the power of these webhook notifications to optimize your dApp or service.



### How to do it?

{% tabs %}
{% tab title="TypeScript / JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

(async () => {
    const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
    
    const monitoredContractAddress = '0xF64E82131BE01618487Da5142fc9d289cbb60E9d'
    
    const monitoredEvent = '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef'
    
    const subscription = await tatum.notification.subscribe.contractAddressLogEvent({
        contractAddress: monitoredContractAddress,
        event: monitoredEvent,
        url: 'https://<YOUR_WEBHOOK_URL>' // replace with your handler URL
    })
    console.log(`Now you will be notified about all monitored event calls on ${monitoredContractAddress}`)
})()
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl -i -X POST \
  https://api.tatum.io/v4/subscription?type=mainnet \
  -H 'Content-Type: application/json' \
  -d '{
    "type": "CONTRACT_ADDRESS_LOG_EVENT",
    "attr": {
      "contractAddress": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
      "chain": "ETH",
      "event": "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
      "url": "https://<YOUR_WEBHOOK_URL>"
    }
  }'
```
{% endcode %}
{% endtab %}
{% endtabs %}

### What does the fired webhook look like?

The fired notification webhook you will receive in your webhook listener will have the following format.

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "events": [
    {
      "txId": "0x7d3dda0430471fe460c07b1ecab35670ef4ce85b",
      "logIndex": 1,
      "timestamp": 1620914417,
      "address": "0x7D3Dda0430471Fe460C07b1ecaB35670eF4ce85b",
      "topic_0": "0x4e3275a5d28e4f6383a4f74592ac9e2f1d0331bde8f7f25cf47d4b15323a47b8",
      "topic_1": "0x000000000000000000000000f64e82131be01618487da5142fc9d289cbb60e9d",
      "topic_2": "0x000000000000000000000000690b9a9e9aa1c9db991c7721a92d351db4fac990",
      "data": "0x0000000000000000000000000000000000000000000000000000000000000064"
    }
  ],
  "blockNumber": 110827114,
  "chain": "ethereum-mainnet",
  "subscriptionType": "CONTRACT_ADDRESS_LOG_EVENT"
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
