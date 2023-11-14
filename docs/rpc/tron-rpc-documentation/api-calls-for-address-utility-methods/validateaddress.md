# validateaddress

### How to use it

Below is an example of how to use the `validateAddress` method with the Tatum SDK:

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

// Initialize the SDK for the TRON network
const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

// Call validateAddress RPC method
const res = await tatum.rpc.validateAddress('TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs', {
  visible: true,
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `validateAddress` method is used to validate the format of a given TRON blockchain address. It verifies if the address is in the correct format, i.e., base58checksum, hexString, or base64 format, and returns a result indicating whether the format is correct or not, along with a message specifying the address format type or an error message.

### Try the call

{% embed url="https://codepen.io/tatum-devrel/pen/zYMXepP" %}

### Parameters

This method accepts the following parameters:

* `address` (string): This is a required parameter. The address should be in base58checksum, hexString, or base64 format.
* `visible` (boolean): Specifies the visibility of the address. It can be set to either true or false. (Optional)

### Return Object

This method returns an object with the following parameters:

* `result` (boolean): Indicates whether the address format is correct.
* `message` (string): Provides the address format type or an error message if the format is incorrect.

### HTTP Request Example

```bash
{
  "address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs",
  "visible": true
}
```

### HTTP Response Example

A successful HTTP response returns a status code of 200 and a JSON body similar to the following example:

```json
{
  "result": true,
  "message": "Base58check format"
}
```

In case of an error, the HTTP response returns a status code of 400 with a body containing an error message.
