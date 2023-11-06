---
description: This page contains information about currently supported authentication types.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Authentication

Access our RPC nodes securely by authenticating with your Tatum account through available methods listed below, ensuring a secure and personalized experience. While it is possible to connect without authentication, please note that this approach provides limited access and functionalities.&#x20;

#### **Init example via SDK**

{% code overflow="wrap" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({
    network: Network.ETHEREUM, 
    apiKey: { v4: 'YOU-API-KEY'}
    }
)
```
{% endcode %}

#### **Basic auth (with base64 encoding)**&#x20;

Please use following base64 format: **x-api-key:\<YOUR-API-KEY>**

{% code overflow="wrap" %}
```json
curl --location 'https://02-dallas-022-01.rpc.tatum.io' 
--header 'Content-Type: application/json' 
--header 'Authorization: Basic eC1...S0x' 
--data '{
    "jsonrpc":"2.0",
    "method":"web3_clientVersion",
    "params":[],
    "id":67
}'
```
{% endcode %}

#### **Auth Bearer**

{% code overflow="wrap" %}
```json
curl --location 'https://02-dallas-022-01.rpc.tatum.io' 
--header 'Content-Type: application/json' 
--header 'Authorization: bearer <YOUR-API-KEY>' 
--data '{
    "jsonrpc":"2.0",
    "method":"web3_clientVersion",
    "params":[],
    "id":1
}'
```
{% endcode %}

#### **X-API-Key set as a user header**

{% code overflow="wrap" %}
```json
curl --location 'https://02-dallas-022-01.rpc.tatum.io'
--header 'Content-Type: application/json' 
--user 'x-api-key:<YOUR-API-KEY>' 
--data '{
    "jsonrpc":"2.0",
    "method":"web3_clientVersion",
    "params":[],
    "id":1
}'
```
{% endcode %}
```json
curl --location 'https://02-dallas-022-01.rpc.tatum.io' 
--header 'Content-Type: application/json' 
--header 'x-api-key:<YOUR-API-KEY>'
--data '{
    "jsonrpc":"2.0",
    "method":"web3_clientVersion",
    "params":[],
    "id":1
}'
```
{% endcode %}

#### **X-API-Key as a part of URL**

{% code overflow="wrap" %}```json
curl --location 'https://x-api-key:<YOUR-API-KEY>@02-dallas-022-01.rpc.tatum.io'
--header 'Content-Type: application/json' 
--data '{
    "jsonrpc":"2.0",
    "method":"web3_clientVersion",
    "params":[],
    "id":1
}'
```
{% endcode %}