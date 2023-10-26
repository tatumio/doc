---
description: >-
  This endpoint allows you to obtain current exchange rate between fiat/crypto
  or fiat/fiat.
---

# Get current exchange rate of the crypto asset

\
The `getExchangeRate()` method offers a seamless way to retrieve up-to-date exchange rate information for cryptocurrencies. By invoking this method, you can effortlessly access the current exchange rate, along with the corresponding timestamp and the reliable source of the data.

### How to use it

<pre class="language-typescript" data-overflow="wrap" data-line-numbers><code class="lang-typescript"><strong>// yarn add @tatumio/tatum
</strong>
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

<strong>const tatum = await TatumSDK.init&#x3C;Ethereum>({network: Network.ETHEREUM})
</strong>
const rate = await tatum.rates.getCurrentRate("BTC","EUR")
</code></pre>

{% embed url="https://codepen.io/tatum-devrel/pen/poQqQNB" %}

### Request Interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
export class RateBatchDto {
  // fiat
  basePair: Fiat

  // crypto currency/fiat
  currency: Fiat | Currency
}
```
{% endcode %}

### Response interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
export class Rate {
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

See the full wide range of fiat currencies we support for the exchange  submodule on this [page](get-current-exchange-rate-of-the-crypto-asset.md#supported-fiat).

### Supported Crypto Currency

See the full wide range of crypto currencies we support for the exchange  submodule on this [page](get-current-exchange-rate-of-the-crypto-asset.md#supported-crypto-currency).
