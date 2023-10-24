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

#### **Basic auth with base64 encoding (base64 format: x-api-key:\<YOUR-API-KEY>)**

{% code overflow="wrap" %}
```
curl -v POST -d "{"jsonrpc": "2.0", "id": "curltest", "method": "getblockchaininfo", "params": []}" -H "content-type: application/json" <https://bitcoin-mainnet-05.rpc.tatum.com> -H "Authorization: Basic YOUR-ENCODED-API-KEY"
```
{% endcode %}

#### **Auth Bearer**

{% code overflow="wrap" %}
```
curl -v POST -d "{"jsonrpc": "2.0", "id": "curltest", "method": "getblockchaininfo", "params": []}" -H "content-type: application/json" <https://bitcoin-mainnet-05.rpc.tatum.io> -H "Authorization: bearer YOUR-API-KEY"
```
{% endcode %}

#### **X-API-Key set as a user header**

{% code overflow="wrap" %}
```
curl -v POST -d "{"jsonrpc": "2.0", "id": "curltest", "method": "getblockchaininfo", "params": []}" -H "content-type: application/json" <https://bitcoin-mainnet-05.rpc.tatum.io> --user "x-api-key:YOUR-API-KEY"
```
{% endcode %}

{% code overflow="wrap" %}
```
curl -v POST -d "{"jsonrpc": "2.0", "id": "curltest", "method": "getblockchaininfo", "params": []}" -H "content-type: application/json" <https://bitcoin-mainnet-05.rpc.tatum.io> --header "x-api-key: YOUR-API-KEY"
```
{% endcode %}

#### **X-API-Key as a part of URL**

{% code overflow="wrap" %}
```
curl -v POST -d "{"jsonrpc": "2.0", "id": "curltest", "method": "getblockchaininfo", "params": []}" -H "content-type: application/json" <https://bitcoin-mainnet-05.rpc.tatum.com> -H "Authorization: Basic YOUR-ENCODED-API-KEY"
```
{% endcode %}
