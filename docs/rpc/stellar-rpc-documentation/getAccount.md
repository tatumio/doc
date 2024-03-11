# getAccount

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the account ID (Replace placeholder with the actual account ID)
const accountId = "YOUR_ACCOUNT_ID";

// Retrieve details of a specific account
const accountDetails = await tatum.rpc.getAccount(accountId);

// Log the account details
console.log("Account Details:", accountDetails);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccount` method allows you to retrieve detailed information about a specific account. This includes information about balances and trustlines, including those that haven't been authorized yet.

### Example use cases:

1. **Account Information:**
   Developers and applications can use this method to access detailed information about a specific account, including its balances and trustlines.

2. **Trustline Analysis:**
   You can use the response to analyze the trustlines established by the account, including those that haven't been authorized yet.

### Request Parameters

The `getAccount` method requires the following parameter:

- `accountId` (string, required):
  The unique identifier (account ID) of the account for which you want to retrieve details.

### Return Object

The `getAccount` method returns a JSON object containing details about the specified account, including balances, sponsorships, and other relevant information.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://horizon.stellar.org/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U"
    },
    "transactions": {
      "href": "https://horizon.stellar.org/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/transactions{?cursor,limit,order}",
      "templated": true
    },
    "operations": {
      "href": "https://horizon.stellar.org/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/operations{?cursor,limit,order}",
      "templated": true
    },
    "payments": {
      "href": "https://horizon.stellar.org/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/payments{?cursor,limit,order}",
      "templated": true
    },
    "effects": {
      "href": "https://horizon.stellar.org/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/effects{?cursor,limit,order}",
      "templated": true
    },
    "offers": {
      "href": "https://horizon.stellar.org/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/offers{?cursor,limit,order}",
      "templated": true
    },
    "trades": {
      "href": "https://horizon.stellar.org/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/trades{?cursor,limit,order}",
      "templated": true
    },
    "data": {
      "href": "https://horizon.stellar.org/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/data/{key}",
      "templated": true
    }
  },
  "id": "GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U",
  "account_id": "GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U",
  "sequence": "24739097524306468",
  "subentry_count": 3,
  "inflation_destination": "GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U",
  "home_domain": "tempo.eu.com",
  "last_modified_ledger": 23569316,
  "num_sponsoring": 0,
  "num_sponsored": 0,
  "thresholds": {
    "low_threshold": 5,
    "med_threshold": 0,
    "high_threshold": 0
  },
  "flags": {
    "auth_required": false,
    "auth_revocable": true,
    "auth_immutable": false,
    "auth_clawback_enabled": true
  },
  "balances": [
    {
      "balance": "1.0000005",
      "limit": "922337203685.4775807",
      "buying_liabilities": "0.0000000",
      "selling_liabilities": "0.0000000",
      "last_modified_ledger": 22651481,
      "is_authorized": true,
      "is_clawback_enabled": false,
      "asset_type": "credit_alphanum4",
      "asset_code": "EURT",
      "asset_issuer": "GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S"
    },
    {
      "balance": "0.0000000",
      "limit": "922337203685.4775807",
      "buying_liabilities": "0.0000000",
      "selling_liabilities": "0.0000000",
      "last_modified_ledger": 7877447,
      "is_authorized": false,
      "is_clawback_enabled": false,
      "asset_type": "credit_alphanum4",
      "asset_code": "PHP",
      "asset_issuer": "GBUQWP3BOUZX34TOND2QV7QQ7K7VJTG6VSE7WMLBTMDJLLAW7YKGU6EP"
    }
  ],
  "signers": [
    {
      "weight": 10,
      "key": "GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U",
      "type": "ed25519_public_key"
    }
  ],
  "data": {},
  "paging_token": ""
}
```
