# nft\_sell\_offers

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const nftId = '00090000D0B007439B080E9B05BF62403911301A7B1F0CFAA048C0A200000007'

const res = await tatum.rpc.nftSellOffers(nftId, { ledgerIndex: 'validated', limit: 250 })

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `nft_sell_offers` method is used to get a list of active sell offers for a specific NFToken. This allows users to track and analyze offers for a particular token and make informed decisions based on the market demand.

{% embed url="https://codepen.io/tatum-devrel/pen/QWJPJZr" %}

### Parameters

* `nftId` (String): The unique identifier of a NFToken object.
* `options` (Ledger & Pagination): Optional parameter that includes details about the ledger to use and pagination options.

### Return Object

\
The `nft_sell_offers` method returns an object that provides information about the sell offers for a specific non-fungible token (NFT). The object contains the following fields:

* `nft_id`: A string that represents the NFT these offers are for, as specified in the request.
* `offers`: An array that contains a list of sell offers for the token. Each member of this array represents one NFTokenOffer object to sell the NFT in question and has the following fields:
  * `amount`: A string or an object that represents the amount offered to sell the NFT for. This could be a string representing an amount in drops of XRP, or an object representing an amount of a fungible token.
  * `flags`: A number that represents a set of bit-flags for this offer. See NFTokenOffer flags for possible values.
  * `nft_offer_index`: A string that represents the ledger object ID of this offer.
  * `owner`: A string that represents the account that placed this offer.
* `limit`: (May be omitted) A number that represents the limit, as specified in the request.
* `marker`: (May be omitted) A server-defined value indicating the response is paginated. Pass this to the next call to resume where this call left off. This field is omitted when there are no pages of information after this one.

### JSON-RPC Request Example

```json
{
  "method": "nft_sell_offers",
  "params": [{
    "nft_id": "00090000D0B007439B080E9B05BF62403911301A7B1F0CFAA048C0A200000007"
  }]
}
```

### JSON-RPC Response Example

```json
{
  "result": {
    "nft_id": "00090000D0B007439B080E9B05BF62403911301A7B1F0CFAA048C0A200000007",
    "offers": [
      {
        "amount": "1000",
        "flags": 1,
        "nft_offer_index": "9E28E366573187F8E5B85CE301F229E061A619EE5A589EF740088F8843BF10A1",
        "owner": "rLpSRZ1E8JHyNDZeHYsQs1R5cwDCB3uuZt"
      }
    ],
    "status": "success"
  }
}
```
