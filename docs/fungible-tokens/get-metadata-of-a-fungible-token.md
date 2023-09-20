# Get metadata of a fungible token

### Overview

Fungible tokens can carry associated metadata, which is a set of data that provides information about the token's properties. Although each token is indistinguishable in value, metadata can specify attributes such as the token's name, symbol, or total supply. In the realm of cryptocurrencies, metadata is often used to create a clearer understanding of the token's purpose or functionality. For instance, a utility token's metadata might detail the specific service or access it provides within its platform. Similarly, a governance token's metadata could illustrate the voting rights or privileges it conveys in a Decentralised Autonomous Organisation (DAO). Thus, metadata provides essential context, enhancing the fungible tokens' usability in diverse scenarios.

{% embed url="https://codepen.io/tatum-devrel/pen/BaGvOoe" %}

### How to show the metadata of a fungible token on the Ethereum network

Use the TatumSDK (`@tatumio/tatum`) to get the token metadata.

{% tabs %}
{% tab title="TypeScript" %}
<pre class="language-typescript" data-overflow="wrap" data-line-numbers><code class="lang-typescript">// yarn add @tatumio/tatum
import { TatumSDK, Network, Ethereum, ResponseDto, TokenMetadata } from '@tatumio/tatum'

const tatum = await TatumSDK.init&#x3C;Ethereum>({network: Network.ETHEREUM})

<strong>const response: ResponseDto&#x3C;TokenMetadata> = await tatum.token.getTokenMetadata({
</strong>        tokenAddress: '0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48',
      })

console.log(response.data)
</code></pre>
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Install with: npm install @tatumio/tatum
const { TatumSDK, Network } = require("@tatumio/tatum");

(async () => {
  try {
    const tatum = await TatumSDK.init({ network: Network.ETHEREUM });
    const result = await tatum.token.getTokenMetadata({
        tokenAddress: '0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48',
      })
      
    console.log(result.data);
  } catch (error) {
    console.error("Error fetching token metadata:", error);
  }
})();
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request GET 'https://api.tatum.io/v4/data/tokens?tokenAddress=0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48&chain=ethereum'
```
{% endcode %}
{% endtab %}
{% endtabs %}

<details>

<summary>Expected Response</summary>

```json5
{
  "symbol":"USDC",
  "name":"USD Coin",
  "supply":"26667389920178985",
  "decimals":6,
  "tokenType":"fungible",
  "cap":"undefined"
}
```

</details>

### Request interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface TokenAddress {
  /**
   * Token contract address
   */
  tokenAddress: string
}
```
{% endcode %}

### Response interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface ResponseDto<T> {
  /**
   * Actual payload of the response
   */
  data: T
  /**
   * Status of the response
   */
  status: Status
  /**
   * In case of ERROR status, this field contains the error message and detailed description
   */
  error?: ErrorWithMessage
}

interface TokenMetadata {
  /**
   * Symbol of the fungible token.
   */
  symbol: string
  /**
   * Full name of the fungible token
   */
  name: string
  /**
   * Total supply of the fungible token.
   */
  supply: string
  /**
   * Number of decimal places for the fungible token.
   */
  decimals: number
  /**
   * Type of the token - fungible
   */
  tokenType: string
  /**
   * Maximum supply cap of the fungible token.
   */
  cap: string
}
```
{% endcode %}

### Supported blockchain networks

| Network                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>Ethereum / Ethereum Sepolia / Ethereum Goerli<br>BNB Smart Chain / BNB Smart Chain Testnet<br>Celo / Celo Alfajores<br>Polygon / Polygon Mumbai</p> |
