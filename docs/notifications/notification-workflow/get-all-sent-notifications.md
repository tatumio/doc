# Get all sent notifications

Getting all sent notifications means retrieving a list of all webhook notifications that have been triggered and sent by the Tatum system to the specified webhook listener URL. This list typically includes information about each fired webhook, such as the event details, timestamp, subscription identifier, and the status of the webhook (e.g., whether it was successfully delivered or encountered an error).

This functionality is useful for maintaining an overview of past webhook events, analyzing the event history, troubleshooting issues, or reconciling data between the Tatum system and your application. By examining the list of fired webhooks, you can gain insights into the events that have occurred on the monitored address(es) and identify any potential issues or discrepancies in your system's handling of these events.

### How to get all sent notifications

When you request to get all fired webhooks using the `tatum.notification.getAllExecutedWebhooks()` operation, the Tatum system returns a collection of webhook events that have been triggered as a result of monitoring the specified blockchain address(es) and detecting events such as balance updates or contract interactions.

{% tabs %}
{% tab title="JavaScript / TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum, Webhook, ResponseDto} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const {status, data}: ResponseDto<Webhook[]> = await tatum.notification.getAllExecutedWebhooks()
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl -i -X GET \
  'https://api.tatum.com/v1/subscription/webhook?pageSize=10&type=mainnet'
```
{% endcode %}
{% endtab %}

{% tab title="C#" %}
```csharp
using System.Text.Json;
using Tatum;
using Tatum.Core;
using Tatum.Notifications.Models.Responses;

// Initialize Tatum SDK
TatumSdk tatumSdk = await TatumSdk.InitAsync();

Result<List<WebhookExecutionResponse>> executedWebhooks = 
  await tatumSdk.Notifications.GetAllExecutedWebhooks();

Console.WriteLine(
  JsonSerializer.Serialize(
    executedWebhooks.Value, 
    new JsonSerializerOptions() { WriteIndented = true}
  )
);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Playing with curl and having a need to define type of net, please, use query parameter `type` with `testnet` or `mainnet` values.\
\
Example:`https://api.tatum.io/v4/subscription/webhook?pageSize=10&type=mainnet`\
\
If you do not use it explicitly `mainnet` is set by default.
{% endhint %}

### Method parameters

The method accepts the optional object with the following properties.

{% tabs %}
{% tab title="JavaScript / TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface GetAllExecutedWebhooksQuery {
  /**
   * The number of items to return per page. Defaults to 10.
   */
  pageSize?: number
  /**
   * The page offset. Defaults to 0.
   */
  offset?: number
  /**
   * Order of the returned items. 'desc' means the most recent items are returned first. Defaults to 'desc'.
   */
  direction?: 'asc' | 'desc'
  /**
   * Filter failed notifications. If the present method will return only successful or failed results based on the filterFailed field.
   */
  filterFailed?: boolean
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Webhook response

The methods response has the following format.

{% tabs %}
{% tab title="JavaScript / TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface Webhook {
  // Type of the subscription
  type: NotificationType
  // Id of the notification
  id: string
  // Id of the subscription
  subscriptionId: string
  // The URL on which is notifications request sent
  url: string
  // The webhook payload
  data: {
    // Monitored address
    address: string
    // Amount of the transaction
    amount: string
    // The asset of the notification
    asset: string
    // The number of the block in which the transaction occurs
    blockNumber: number
    // Transaction hash
    txId: string
    // Type of the notification
    type: string
    // Network of the notification
    chain: string
    // Type of the subscription
    subscriptionType: NotificationType
  }
  // Next notification execution try time	- Unix timestamp
  nextTime: number
  // Notification execution time - Unix timestamp
  timestamp: number
  // Number of retries in case of the failed attempts in the past
  retryCount: number
  // Flag indicating whether this notification was successful or not	
  failed: boolean
  // Response from the server in case the notification was unsuccessful
  response: {
    code: number
    data: string
    networkError: boolean
  }
}

```
{% endcode %}
{% endtab %}
{% endtabs %}

### Example

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "id": "64133ffb2367c7fb4fdeb0cf",
  "subscriptionId": "64133c4b2aef5483132f9d40",
  "url": "https://dashboard.tatum.io/webhook-handler",
  "type": "FAILED_TXS_PER_BLOCK",
  "data": {
    "address": "0x3a88ededf304949c46d1380f6960bc1de94b9dcf",
    "amount": "0",
    "asset": "KLAY",
    "blockNumber": 117406122,
    "counterAddress": "0xfdeedbb2fe5b48d5b49e435ba00e0358740d0cf5",
    "txId": "0xa3d2bb94d1faf6e3ae85c869e73cbb8eedb73f0b0feb35601e982c087c2e3f91",
    "type": "native",
    "chain": "klaytn-baobab",
    "subscriptionType": "FAILED_TXS_PER_BLOCK",
  },
  "nextTime": 1678983161545,
  "timestamp": 1678983163000,
  "retryCount": 2,
  "failed": true,
  "response": {
    "code": 404,
    "data": "NOT FOUND",
    "networkError": false
  }
}
```
{% endcode %}
