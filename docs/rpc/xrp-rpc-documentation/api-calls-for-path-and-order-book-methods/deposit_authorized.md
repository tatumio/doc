# deposit\_authorized

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const sourceAccount = 'rEhxGqkqPPSxQ3P25J66ft5TwpzV14k2de'
const destinationAccount = 'rsUiUMpnrgxQp24dJYZDhmV4bE3aBtQyt8'

const res = await tatum.rpc.depositAuthorized(sourceAccount, destinationAccount, { ledgerIndex: 'validated' })

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `deposit_authorized` method is used to verify if a specific account is authorized to send payments to another account. This feature becomes particularly useful in scenarios where accounts have deposit authorization enabled, which is a setting that requires accounts to be preauthorized before they can send payments.

### Parameters

* `sourceAccount` (String): The sender of a possible payment.
* `destinationAccount` (String): The recipient of a possible payment.
* `options` (Ledger): Optional parameter that includes details about the ledger to use.

### Return Object

The `deposit_authorized` method returns an object that provides information about whether the specified source account is authorized to send payments directly to the destination account. The object contains the following fields:

* `deposit_authorized`: A boolean indicating whether the specified source account is authorized to send payments directly to the destination account. If true, either the destination account does not require Deposit Authorization or the source account is preauthorized.
* `destination_account`: A string that represents the destination account specified in the request.
* `ledger_hash`: (May be omitted) A string that represents the identifying hash of the ledger that was used to generate this response.
* `ledger_index`: (May be omitted) A number that represents the ledger index of the ledger version that was used to generate this response.
* `ledger_current_index`: (May be omitted) A number that represents the ledger index of the current in-progress ledger version, which was used to generate this response.
* `source_account`: A string that represents the source account specified in the request.
* `validated`: (May be omitted) A boolean indicating whether the information comes from a validated ledger version. If true, the information comes from a validated ledger version.

### JSON-RPC Request Example

```json
{
  "method": "deposit_authorized",
  "params": [
    {
      "source_account": "rEhxGqkqPPSxQ3P25J66ft5TwpzV14k2de",
      "destination_account": "rsUiUMpnrgxQp24dJYZDhmV4bE3aBtQyt8",
      "ledger_index": "validated"
    }
  ]
}
```

### JSON-RPC Response Example

```json
{
  "result": {
    "deposit_authorized": true,
    "destination_account": "rsUiUMpnrgxQp24dJYZDhmV4bE3aBtQyt8",
    "ledger_hash": "BD03A10653ED9D77DCA859B7A735BF0580088A8F287FA2C5403E0A19C58EF322",
    "ledger_index": 8,
    "source_account": "rEhxGqkqPPSxQ3P25J66ft5TwpzV14k2de",
    "status": "success",
    "validated": true
  }
}
```
