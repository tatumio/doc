# Notification workflow

Webhooks are automated messages sent from applications when certain events occur. In this case, the TatumSDK webhook system enables you to receive notifications about balance update events for a specific Ethereum address. To better understand the workflow, let's break it down into steps and present it in a simple guide. Then, we'll add a UML diagram to visualise the process.

### Webhook Workflow Guide

1. **Create a subscription**: Use the TatumSDK (@tatumio/tatum) to create a subscription for address events.

{% tabs %}
{% tab title="JavaScript / TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const subscription = await tatum.notification.subscribe.addressEvent({
  address: '0xF64E82131BE01618487Da5142fc9d289cbb60E9d', // replace with your address
  url: 'https://<YOUR_WEBHOOK_URL>' // replate with your URL handler
});
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
<pre class="language-bash" data-overflow="wrap" data-line-numbers><code class="lang-bash"><strong>curl -i -X POST \
</strong>  https://api.tatum.io/v4/subscription?type=mainnet \
  -H 'Content-Type: application/json' \
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

This function returns an object with an `id` property - a string identifier of the created subscription.

{% hint style="info" %}
Playing with curl and having a need to define type of net, please, use query parameter `type` with `testnet` or `mainnet` values.\
\
Example: `https://api.tatum.io/v4/subscription?type=mainnet`\
\
If you do not use it explicitly `mainnet` is set by default.
{% endhint %}

2. **Monitor the address**: Tatum starts monitoring the specified address for any balance update events happening on the Ethereum blockchain.
3. **Trigger the webhook**: Once Tatum detects an event, it fires a notification as an HTTP POST request to the webhook listener URL defined in the subscription. The request includes a JSON payload with the event details. Should you have specific access controls in place, you can whitelist these Tatum IP addresses ([TXT](https://ips.tatum.com/ips.txt) | [JSON](https://ips.tatum.com/ips.json)) that will fire requests to your application.&#x20;
4. **Unsubscribe from the notification**: The user can unsubscribe from the notification by calling `tatum.notification.unsubscribe(id)`.
5. **List fired webhooks**: Users can list all fired webhooks by calling the `tatum.notification.getAllExecutedWebhooks()` operation.

### UML Diagram

Here's a UML diagram that focuses on the flow of subscribing, receiving events, and firing notifications. Code examples are included in the boxes for each step.

```css
+------------------------+          +------------------------+
|                        |          |                        |
|   1. User Subscribes   |          |   2. Monitor Address   |
|                        |          |                        |
|   Code example:        |          |   (Handled by Tatum)   |
|                        |          |                        |
| tatum.notification     |          +-----------+------------+
|  .subscribe            |                      |
|  .addressEvent({       +--------------------->|
|   address: '0xF64E8...'|                      |
|   url: 'https://das...'|                      |
| });                    |                      |
+------------------------+                      |
                                                |
  +---------------------+                       |
  |                     |                       |
  |  Event Detected on  |<----------------------+
  |  the Address        +---------------------->|
  +---------------------+                       |
                                                |
                                                |
                                                |
                                                v
                                     +----------+----------+
                                     |                     |
                                     | 3. Process Event    |
                                     | (Tatum) &           |
                                     | Fire                |
                                     | Notification        |
                                     |                     |
                                     | (Handled by         |
                                     | Webhook             |
                                     | Listener)           |
                                     |                     |
                                     | Example             |
                                     | Payload:            |
                                     | {                   |
                                     |  "type": "BALANCE", |
                                     |  "amount": "0.5"    |
                                     | }                   |
                                     +---------------------+
```

In this diagram, the following steps are shown:

1. **Create subscription**: The user creates a subscription using the TatumSDK with the specified address and webhook listener URL.

{% tabs %}
{% tab title="JavaScript / TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum} from '@tatumio/tatum'

const tatum = TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const subscription = await tatum.notification.subscribe.addressEvent({
  address: '0xF64E82131BE01618487Da5142fc9d289cbb60E9d', // replace with your address
  url: 'https://<YOUR_WEBHOOK_URL>' // replate with your URL handler
});
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
<pre class="language-bash"><code class="lang-bash"><strong>curl -i -X POST \
</strong>  https://api.tatum.io/v4/subscription?type=mainnet \
  -H 'Content-Type: application/json' \
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

2. **Monitor Address**: Tatum monitors the specified address for balance update events happening on the Ethereum blockchain.
3. **Receive & Fire Notification**:  The webhook listener receives the event and processes the notification. An example JSON payload is provided in the diagram. Should you have specific access controls in place, you can whitelist these Tatum IP Addresses ([TXT](https://ips.tatum.com/ips.txt) | [JSON](https://ips.tatum.com/ips.json)) that will fire requests to your application.

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
  "amount": "0.001",
  "asset": "ETH",
  "blockNumber": 2913059,
  "counterAddress": "0x690B9A9E9aa1C9dB991C7721a92d351Db4FaC990",
  "txId": "0x062d236ccc044f68194a04008e98c3823271dc26160a4db9ae9303f9ecfc7bf6",
  "type": "native",
  "chain": "ethereum-mainnet",
  "subscriptionType": "ADDRESS_EVENT"
}
```
{% endcode %}
