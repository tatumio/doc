# account\_tx

### How to use It

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.accountTx('rLNaPoKeeBjZe2qs6x52yVPZpZ8td4dc6w', {
  ledgerIndexMin: -1,
  ledgerIndexMax: -1,
  binary: false,
  forward: false,
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `account_tx` method is a part of the XRP Ledger's RPC API, allowing you to retrieve a list of transactions that involve a specified account. This method is useful when you need to track and analyze transactions related to a particular account, which can be necessary for various operations such as auditing, debugging or just for general monitoring purposes.

{% embed url="https://codepen.io/tatum-devrel/pen/abQxaqm" %}

### Parameters

The `accountTx` method accepts the following parameters:

* `account`: A unique identifier for the account, most commonly the account's address.
* `ledgerIndexMin`: (Optional) Use to specify the earliest ledger to include transactions from. A value of -1 instructs the server to use the earliest validated ledger version available.
* `ledgerIndexMax`: (Optional) Use to specify the most recent ledger to include transactions from. A value of -1 instructs the server to use the most recent validated ledger version available.
* `binary`: (Optional) Defaults to false. If set to true, returns transactions as hex strings instead of JSON.
* `forward`: (Optional) Defaults to false. If set to true, returns values indexed with the oldest ledger first. Otherwise, the results are indexed with the newest ledger first.

### Return Object

The response object includes the following fields:

* `account`: Unique Address identifying the related account.
* `ledger_index_min`: The ledger index of the earliest ledger actually searched for transactions.
* `ledger_index_max`: The ledger index of the most recent ledger actually searched for transactions.
* `limit`: The limit value used in the request.
* `marker`: Server-defined value indicating the response is paginated.
* `transactions`: Array of transactions matching the request's criteria.
* `validated`: If included and set to true, the information in this response comes from a validated ledger version.

Each transaction object includes the following fields:

* `ledger_index`: The ledger index of the ledger version that included this transaction.
* `meta`: If binary is True, then this is a hex string of the transaction metadata. Otherwise, the transaction metadata is included in JSON format.
* `tx`: (JSON mode only) JSON object defining the transaction.
* `validated`: Whether or not the transaction is included in a validated ledger.

### JSON-RPC Request Example

```json
{
  "method": "account_tx",
  "params": [
    {
      "account": "rLNaPoKeeBjZe2qs6x52yVPZpZ8td4dc6w",
      "binary": false,
      "forward": false,
      "ledger_index_max": -1,
      "ledger_index_min": -1,
      "limit": 2
    }
  ]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "account": "rLNaPoKeeBjZe2qs6x52yVPZpZ8td4dc6w",
        "ledger_index_max": 57112019,
        "ledger_index_min": 56248229,
        "limit": 2,
        "marker": {
            "ledger": 57112007,
            "seq": 13
        },
        "status": "success",
        "transactions": [
            {
                "meta": {
                    "AffectedNodes": [
                        {
                            "ModifiedNode": {
                                "FinalFields": {
                                    "Account": "rLNaPoKeeBjZe2qs6x52yVPZpZ8td4dc6w",
                                    "Balance": "3732290013101",
                                    "Flags": 131072,
                                    "OwnerCount": 0,
                                    "Sequence": 702820
                                },
                                "LedgerEntryType": "AccountRoot",
                                "LedgerIndex": "140FA03FE8C39540CA8189BC7A7956795C712BC0A542C6409C041150703C8574",
                                "PreviousFields": {
                                    "Balance": "3732745656171",
                                    "Sequence": 702819
                                },
                                "PreviousTxnID": "7C031FD5B710E3C048EEF31254089BEEC505900BCC9A842257A0319453333998",
                                "PreviousTxnLgrSeq": 57112010
                            }
                        },
                        {
                            "ModifiedNode": {
                                "FinalFields": {
                                    "Account": "raLPjTYeGezfdb6crXZzcC8RkLBEwbBHJ5",
                                    "Balance": "4231510602153",
                                    "Flags": 0,
                                    "OwnerCount": 0,
                                    "Sequence": 96486
                                },
                                "LedgerEntryType": "AccountRoot",
                                "LedgerIndex": "39DC5D448DECEFC3CD20818788E3DA891CA943935E8D7B12FCB5B5871FCB1638",
                                "PreviousFields": {
                                    "Balance": "4231054959123"
                                },
                                "PreviousTxnID": "33D2014C832610293730028CA37857AC183BFCE3E42B9979C491FB8B82B3E9DC",
                                "PreviousTxnLgrSeq": 57112004
                            }
                        }
                    ],
                    "TransactionIndex": 12,
                    "TransactionResult": "tesSUCCESS",
                    "delivered_amount": "455643030"
                },
                "tx": {
                    "Account": "rLNaPoKeeBjZe2qs6x52yVPZpZ8td4dc6w",
                    "Amount": "455643030",
                    "Destination": "raLPjTYeGezfdb6crXZzcC8RkLBEwbBHJ5",
                    "DestinationTag": 18240312,
                    "Fee": "40",
                    "Flags": 2147483648,
                    "LastLedgerSequence": 57112037,
                    "Sequence": 702819,
                    "SigningPubKey": "020A46D8D02AC780C59853ACA309EAA92E7D8E02DD72A0B6AC315A7D18A6C3276A",
                    "TransactionType": "Payment",
                    "TxnSignature": "30450221008602B2E390C0C7B65182C6DBC86292052C1961B2BEFB79C2C8431722C0ADB911022024B74DCF910A4C8C95572CF662EB7F5FF67E1AC4D7B9B7BFE2A8EE851EC16576",
                    "date": 649200322,
                    "hash": "08EF5BDA2825D7A28099219621CDBECCDECB828FEA202DEB6C7ACD5222D36C2C",
                    "inLedger": 57112015,
                    "ledger_index": 57112015
                },
                "validated": true
            },
            {
                "meta": {
                    "AffectedNodes": [
                        {
                            "ModifiedNode": {
                                "FinalFields": {
                                    "Account": "rLNaPoKeeBjZe2qs6x52yVPZpZ8td4dc6w",
                                    "Balance": "3732745656171",
                                    "Flags": 131072,
                                    "OwnerCount": 0,
                                    "Sequence": 702819
                                },
                                "LedgerEntryType": "AccountRoot",
                                "LedgerIndex": "140FA03FE8C39540CA8189BC7A7956795C712BC0A542C6409C041150703C8574",
                                "PreviousFields": {
                                    "Balance": "3732246155784"
                                },
                                "PreviousTxnID": "CCBCCB528F602007C937C496F0828C118E073DF180084CCD3646EC1E414844E4",
                                "PreviousTxnLgrSeq": 57112007
                            }
                        },
                        {
                            "ModifiedNode": {
                                "FinalFields": {
                                    "Account": "rw2ciyaNshpHe7bCHo4bRWq6pqqynnWKQg",
                                    "Balance": "236476361",
                                    "Flags": 131072,
                                    "OwnerCount": 0,
                                    "Sequence": 466335
                                },
                                "LedgerEntryType": "AccountRoot",
                                "LedgerIndex": "CC20FEBEA6D2AF969EC46F2BD92684D9FBABC3F238E841B5E056FE4EBF4379A9",
                                "PreviousFields": {
                                    "Balance": "735976788",
                                    "Sequence": 466334
                                },
                                "PreviousTxnID": "C528B32DD588EFAE2FE833E8AA92E6AE2DF2C8DB3DB8C6C4F334AD37B253D72A",
                                "PreviousTxnLgrSeq": 57112010
                            }
                        }
                    ],
                    "TransactionIndex": 33,
                    "TransactionResult": "tesSUCCESS",
                    "delivered_amount": "499500387"
                },
                "tx": {
                    "Account": "rw2ciyaNshpHe7bCHo4bRWq6pqqynnWKQg",
                    "Amount": "499500387",
                    "Destination": "rLNaPoKeeBjZe2qs6x52yVPZpZ8td4dc6w",
                    "DestinationTag": 1,
                    "Fee": "40",
                    "Flags": 2147483648,
                    "LastLedgerSequence": 57112032,
                    "Sequence": 466334,
                    "SigningPubKey": "0381575032E254BF4D699C3D8D6EFDB63B3A71F97475C6F6885BC7DAEEE55D9A01",
                    "TransactionType": "Payment",
                    "TxnSignature": "3045022100C7EA1701FE48C75508EEBADBC9864CD3FFEDCEB48AB99AEA960BFA360AE163ED0220453C9577502924C9E1A9A450D4B950A44016813BC70E1F16A65A402528D730B7",
                    "date": 649200302,
                    "hash": "7C031FD5B710E3C048EEF31254089BEEC505900BCC9A842257A0319453333998",
                    "inLedger": 57112010,
                    "ledger_index": 57112010
                },
                "validated": true
            }
        ],
        "validated": true
    }
}
```
