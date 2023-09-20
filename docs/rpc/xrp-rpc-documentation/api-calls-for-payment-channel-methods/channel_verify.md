# channel\_verify

### How to use it

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.channelVerify(
  '1000000',
  '5DB01B7FFED6B67E6B0414DED11E051D2EE2B7619CE0EAA6286D67A3A4D5BDB3',
  'aB44YfzW24VDEJQ2UuLPV2PvqcPCSoLnL7y5M1EzhdW4LnK5xMS3',
  '304402204EF0AFB78AC23ED1C472E74F4299C0C21F1B21D07EFC0A3838A420F76D783A400220154FB11B6F54320666E4C36CA7F686C16A3A0456800BBC43746F34AF50290064'
)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `channel_verify` method is used to check the validity of a signature that can be used to redeem a specific amount of XRP from a payment channel. This method was added by the PayChan amendment and is available starting from the `rippled` 0.33.0 version.

The main use case of this method is to confirm the validity of a claim before attempting to redeem it. This is especially useful for payment channel recipients who want to ensure they are receiving valid claims.

### Parameters

The `channel_verify` method includes the following parameters:

* `amount`: The amount of XRP, in drops, the provided signature authorizes.
* `channelId`: The Channel ID of the channel that provides the XRP. This is a 64-character hexadecimal string.
* `publicKey`: The public key of the channel and the key pair that was used to create the signature, in hexadecimal or the XRP Ledger's base58 format.
* `signature`: The signature to verify, in hexadecimal.

### Return Object

The `channel_verify` method returns a result object that includes:

* `signature_verified`: If true, the signature is valid for the stated amount, channel, and public key.

> **Caution:** This does not indicate check that the channel has enough XRP allocated to it. Before considering a claim valid, you should look up the channel in the latest validated ledger and confirm that the channel is open and its amount value is equal or greater than the amount of the claim. To do so, use the `account_channels` method.

### JSON-RPC Request Example

```json
{
    "method": "channel_verify",
    "params": [{
        "channel_id": "5DB01B7FFED6B67E6B0414DED11E051D2EE2B7619CE0EAA6286D67A3A4D5BDB3",
        "signature": "304402204EF0AFB78AC23ED1C472E74F4299C0C21F1B21D07EFC0A3838A420F76D783A400220154FB11B6F54320666E4C36CA7F686C16A3A0456800BBC43746F34AF50290064",
        "public_key": "aB44YfzW24VDEJQ2U

uLPV2PvqcPCSoLnL7y5M1EzhdW4LnK5xMS3",
        "amount": "1000000"
    }]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "signature_verified":true,
        "status":"success"
    }
}
```
