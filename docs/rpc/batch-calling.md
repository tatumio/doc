---
description: >-
  This page provides info on making batch calls to our RPC nodes, enabling
  efficient and simultaneous requests. Batch calling is useful for scenarios
  requiring data from multiple blocks or transaction.
---

# Batch Calling

## **Overview**

Batch calling allows you to send multiple JSON-RPC requests in a single API call. This method is efficient for retrieving or sending data to multiple endpoints in one network request, streamlining your interactions with the blockchain.

> Note :&#x20;
>
> 1. Batch Request is only available for enterprise users.
> 2. This feature requires the use of the SDK with an API key.&#x20;
> 3. All batch requests are processed as raw node requests.

## Init Example via SDK

For batch calling, you can use our SDK to simplify the process. Here's an example of initialising the SDK for batch requests:

```javascript
const { TatumSDK, Network } = require('@tatumio/tatum');

const tatum = await TatumSDK.init({
    network: Network.ETHEREUM, 
    apiKey: { v4: 'YOUR-API-KEY'}
    }
)
```

## Batch Call Format

A batch call is a JSON array containing multiple JSON-RPC request objects. Each object in the array is a separate request, following the standard JSON-RPC request format.

## Preparing the request

The rawBatchRpcCall function expects request as an array of request objects, where each request is a standard rpc request.

```bash
[{
    "jsonrpc":"2.0",
    "method":"METHOD_NAME",
    "params":[PARAMS],
    "id":1
}, {
    // Additional request
}]'
```

## Making the Batch Request :&#x20;

```javascript
const { TatumSDK, Network } = require('@tatumio/tatum');

(async () => {
const tatum = await TatumSDK.init({
    network: Network.ETHEREUM, 
    apiKey: { v4: 'YOUR-API-KEY'}
    }
)

request = [{
      "jsonrpc": "2.0",
      "id": 1,
      "method": "eth_blockNumber"
    },
    {
      "jsonrpc": "2.0",
      "id": 2,
      "method": "eth_getBlockByNumber",
      "params": [
        "latest",
        true
        ]
    }]
  
const batchRequest = await tatum.rpc.rawBatchRpcCall(request);
console.log(batchRequest)

})();
```

## Best Practices

* Ensure that each request in the batch has a unique ID.
* Verify the format and parameters of each request to avoid errors.
* Consider the server load and rate limits when making batch calls.
