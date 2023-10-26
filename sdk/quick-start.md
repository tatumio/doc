---
description: Fastest SDK to get you started
---

# 🚀 Quick Start

### :package: Install the SDK :package:

{% tabs %}
{% tab title="TypeScript / JavaScript SDK" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
npm install @tatumio/tatum
```
{% endcode %}
{% endtab %}
{% endtabs %}

### :gear: Make your first RPC call :gear:

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

// Init chain of your choice
 const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
 
 // Use our interfaces to make the call
 const latestBlock = await tatum.rpc.blockNumber()
 
 console.log(`Latest block is ${latestBlock}`)

```
{% endcode %}
{% endtab %}
{% endtabs %}
