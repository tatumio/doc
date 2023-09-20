# Get all existing monitoring subscriptions

Getting all existing monitoring subscriptions means retrieving a list of all the active webhook subscriptions that have been created through Tatum. Each subscription in the list represents a blockchain address being monitored for events, such as balance updates or contract interactions, along with the associated webhook listener URL to which the notifications are sent.

When you request to get all existing monitoring subscriptions, Tatum returns a collection of subscription objects. Each object typically includes information such as the subscription identifier, the monitored blockchain address, the webhook listener URL, and any additional configuration or filters applied to the subscription.

This functionality is useful for managing and reviewing your current webhook subscriptions, allowing you to keep track of which addresses are being monitored and the corresponding webhook listener URLs. By examining the list of existing subscriptions, you can ensure that you have the desired monitoring configurations in place and make any necessary adjustments or updates to your webhook subscriptions.

### How to get all existing/active notifications

When you request to get all active notifications using the `tatum.notification.`getAll`()` operation, Tatum returns a collection of active notifications that you have for monitoring the specified blockchain address(es) and detecting events such as balance updates or contract interactions.

{% tabs %}
{% tab title="JavaScript / TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum, NotificationSubscription, ResponseDto} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const {status, data}: ResponseDto<NotificationSubscription[]> = await tatum.notification.getAll()
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl -i -X GET \
  'https://api.tatum.io/v4/subscription?pageSize=10&type=mainnet'
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Playing with curl and having a need to define type of net, please, use query parameter `type` with `testnet` or `mainnet` values.\
\
Example: `https://api.tatum.io/v4/subscription?pageSize=10&type=mainnet`\
\
If you do not use it explicitly `mainnet` is set by default.
{% endhint %}

### Method parameters

The method accepts the optional object with the following properties.

{% tabs %}
{% tab title="JavaScript / TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface GetAllSubscriptionsQuery {
  /**
   * Number of records to return. The default is 10.
   */
  pageSize?: number
  /**
   * Number of records to skip. The default is 0.
   */
  offset?: number
  /**
   * Address to filter by.
   */
  address?: string
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Subscription response

The methods response has the following format.

{% tabs %}
{% tab title="JavaScript / TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface NotificationSubscription {
  /**
   * ID of a subscription.
   */
  id: string
  /**
   * Blockchain network.
   */
  network: Network
  /**
   * URL of the webhook listener.
   */
  url: string
  /**
   * Type of notification subscription.
   */
  type: NotificationType
  /**
   * Address to monitor, valid for some of the types only.
   */
  address?: string
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
