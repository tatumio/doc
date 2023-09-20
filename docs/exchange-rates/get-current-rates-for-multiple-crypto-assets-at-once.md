---
description: >-
  This endpoint allows you to obtain current exchange rates between fiat/crypto
  or fiat/fiat.
---

# Get current rates for multiple crypto assets at once

\
The `getExchangeRates()` method in our API provides a powerful solution similar to the "Get current rate" method. It enables you to obtain current exchange rate information, along with timestamps and the source of the data. \
\
One notable feature of this method is the ability to request multiple exchange pairs simultaneously. This means you can retrieve exchange rates for various cryptocurrencies all in one API call, saving time and reducing complexity.

### How to use it

<pre class="language-typescript" data-overflow="wrap" data-line-numbers><code class="lang-typescript"><strong>// yarn add @tatumio/tatum
</strong>
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init&#x3C;Ethereum>({network: Network.ETHEREUM})

const rates = tatum.rates.getCurrentRateBatch(
      [{
        currency: "BTC",
        basePair: "EUR",
        batchId: "0"
      }, {
        currency: "ETH",
        basePair: "EUR",
        batchId: "1"
      }])
</code></pre>

{% embed url="https://codepen.io/tatum-devrel/pen/xxQmQgV" %}

### Request Interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// array of
export class RateBatchDto {
  // fiat
  basePair: Fiat

  // crypto currency/fiat
  currency: Fiat | Currency

  // used to identify pair in batch calls
  batchId?: string
}
```
{% endcode %}

### Response interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// array of
export class Rate {
  // used to identify pair in batch calls
  batchId?: string

  // crypto currency/fiat
  _id: Fiat | Currency

  // the amount of basePair that can be exchanged for 1 _id (crypto currency/fiat)
  value: string

  // fiat
  basePair: Fiat

  // timestamp of rate information from source
  timestamp: number

  // source of rate
  source: string
}

```
{% endcode %}

### Supported FIAT

See the full wide range of fiat currencies we support for the exchange  submodule on this [page](get-current-rates-for-multiple-crypto-assets-at-once.md#supported-fiat).

### Supported Crypto Currency

See the full wide range of crypto currencies we support for the exchange  submodule on this [page](get-current-rates-for-multiple-crypto-assets-at-once.md#supported-crypto-currency).
