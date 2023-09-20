# broadcasttransaction

### How to use it

Below is an example of how to use the `broadcastTransaction` method with the Tatum SDK:

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// Install Tatum SDK
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

// Initialize the SDK for the TRON network
const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

// Define a transaction raw body
const rawBody = {
    // fill out appropriate data
}

// Call broadcastTransaction RPC method
const res = await tatum.rpc.broadcastTransaction(rawBody);

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `broadcastTransaction` method is used to broadcast a raw transaction to the TRON blockchain network. It submits the transaction for inclusion in the blockchain and returns the result of the broadcast attempt, including the transaction id and any error information.

### Parameters

This method accepts a single parameter, `rawBody`, which is a `TronTxRawBody` object with the following properties:

* `txID` (string): Transaction identifier.
* `visible` (boolean): Specifies the visibility of the transaction. It can be set to either true or false.
* `raw_data` (json): Raw data of the transaction.
* `raw_data_hex` (string): Raw data of the transaction in hexadecimal format.
* `signature` (array of strings): Array of signatures for the transaction.

### Return Object

This method returns a Promise resolving to an object with the following parameters:

* `result` (boolean): Indicates whether the broadcast was successful. If the broadcast failed, this field will not be displayed in the returned result.
* `txid` (string): Transaction id.
* `code` (string): Error code, present if the broadcast failed.
* `message` (string): Detailed error information, present if the broadcast failed.

### HTTP Request Example

JSON request body example:

```json
{
  "raw_data": "{\"contract\":[{\"parameter\":{\"value\":{\"amount\":1000,\"owner_address\":\"41608f8da72479edc7dd921e4c30bb7e7cddbe722e\",\"to_address\":\"41e9d79cc47518930bc322d9bf7cddd260a0260a8d\"},\"type_url\":\"type.googleapis.com/protocol.TransferContract\"},\"type\":\"TransferContract\"}],\"ref_block_bytes\":\"5e4b\",\"ref_block_hash\":\"47c9dc89341b300d\",\"expiration\":1591089627000,\"timestamp\":1591089567635}",
  "raw_data_hex": "<0a025e4b220847c9dc89341b300d40f8fed3a2a72e5a66080112620a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412310a1541608f8da72479edc7dd921e4c30bb7e7cddbe722e121541e9d79cc47518930bc322d9bf7cddd260a0260a8d18e8077093afd0a2a72e>"
}
```

### HTTP Response Example

A successful HTTP response returns a JSON body similar to the following example:

```json
{
  "result": true,
  "txid": "77ddfa7093cc5f745c0d3a54abb89ef070f983343c05e0f89e5a52f3e5401299"
}
```

In case of an error, the HTTP response returns a JSON body with an error message:

```json
{
  "code": "SIGERROR",
  "txid": "77ddfa7093cc5f745c0d3a54abb89ef070f983343c05e0f89e5a52f3e5401299",
  "message": "56616c6964617465207369676e6174757265206572726f723a206d69737320736967206f7220636f6e7472616374"
}
```
