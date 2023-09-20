# Configuration options

### Network

Every Tatum SDK instance must be initiated with the proper blockchain network. All operations performed later using this SDK will automatically use the network from the configuration.

{% hint style="info" %}
To see the list of all available blockchain protocols, check on [GitHub](https://github.com/tatumio/tatum-js/blob/master/src/dto/Network.ts).
{% endhint %}

{% code overflow="wrap" lineNumbers="true" %}
```typescript
import {TatumSDK, Network, Ethereum} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
```
{% endcode %}

{% hint style="success" %}
TatumSDK is returning the correct types for the RPC submodule using generic types in the init() method. To see all the supported RPC types, check [here](https://github.com/tatumio/tatum-js/blob/master/src/dto/rpc/index.ts).
{% endhint %}

### API Version

Tatum SDK works with two versions of the Tatum API - version 3 and version 4. Each of the versions supports different operations, it's recommended to use version 4.

{% hint style="info" %}
Version 4 of the API supports the most up-to-date features and is set as a default value. The SDK by default tries to perform the calls against version 4 and fallbacks to version 3
{% endhint %}

{% code lineNumbers="true" %}
```typescript
import {TatumSDK, Network, Ethereum, ApiVersion} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM, version: ApiVersion.V4})
```
{% endcode %}

### API Key

Most of the operations available in the SDK don't require API Key authentication to Tatum. But, if you want to have a higher throughput or save your data for future use, you should obtain one at [Tatum Dashboard](https://dashboard.tatum.com). Here, you will get the API Key Version 4 for your SDK, and you can use it in your application.

{% hint style="info" %}
Alternatively, for access to features of Api Key Version 3, you can get the API Key [here](https://dashboard.tatum.io).

You can use both API Keys at the same time or just one of them.
{% endhint %}

{% code overflow="wrap" lineNumbers="true" %}
```typescript
import {TatumSDK, Network, Ethereum} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({
  network: Network.ETHEREUM,
  apiKey: {
   v3: 'YOUR_API_KEY_V3',
   v4: 'YOUR_API_KEY_V4'
})
```
{% endcode %}

### Verbose mode

If you want to start the verbose logging mode to see requests and responses returned from the Tatum API, just set the config `verbose: true`.

{% code overflow="wrap" lineNumbers="true" %}
```typescript
import {TatumSDK, Network, Ethereum} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM, verbose: true})
```
{% endcode %}

### Custom RPC provider URL

You can use any RPC provider for interacting with a blockchain. Just add your custom node provider inside `rpc.nodes` array. All other features from the SDK will work as expected, only the RPC calls will point to your custom node.

{% code overflow="wrap" lineNumbers="true" %}
```typescript
import {TatumSDK, Network, Ethereum} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM, rpcUrl: 'https://YOUR_CUSTOM_RPC_PROVIDER'})

const tatum = await TatumSDK.init<BaseEvmClass>({
    network: Network.ETHEREUM,
    verbose: true,
    rpc: {
       nodes: [
         {
           url: 'YOUR_CUSTOM_PROVIDER_URL',
           type: RpcNodeType.NORMAL,
        },
      ],
    },
})
```
{% endcode %}

### Retry

There are some cases when requests fail to complete successfully. For instance, when you exceed request rate limitations or a network error occurs. To configure behavior when requests fail use

* `retryCount` - specifies the maximum number of how many times the failed request is resent again until a successful response is returned, the default value is 1
* `retryDelay` - specifies the number in milliseconds of how long it waits before the failed request is resent again, the default value is 1000

{% code overflow="wrap" lineNumbers="true" %}
```typescript
import {TatumSDK, Network, Ethereum} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({
    network: Network.ETHEREUM, 
    retryCount: 5,
    retryDelay: 1500,
})
```
{% endcode %}
