# getTransactions

## How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values)
const params = {
    cursor: 'YOUR_CURSOR',
    order: 'asc',
    limit: 10,
    includeFailed: true
};

// Get a list of transactions
const transactions = await tatum.rpc.getTransactions(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

## Overview

The `getTransactions` method allows you to retrieve a list of transactions on the Stellar blockchain. You can use this method in streaming mode to listen for new transactions as they are added to the Stellar ledger. When used in streaming mode, Horizon will start at the earliest known transaction unless a cursor is set, in which case it will start from that cursor. By setting the cursor value to now, you can stream transactions created since your request time.

## Example use cases:

1. **Transaction Monitoring:**
   Developers and applications can use this method to monitor and track all transactions on the Stellar network in real-time.

2. **Transaction Data Analysis:**
   Users can retrieve a list of transactions for analysis, reporting, and auditing purposes.

3. **Stream Transactions:**
   You can use streaming mode to receive real-time updates of new transactions on the Stellar ledger.

## Request Parameters

The `getTransactions` method accepts the following optional parameters:

- `cursor` (string, optional):
  An optional cursor to start listing transactions from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of transactions to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional):
  An optional parameter to include failed transactions. If set to true, failed transactions will be included in the results. Defaults to false.

## Return Object

The `getTransactions` method returns an array of transactions on the Stellar blockchain. Each transaction object contains information such as the transaction ID, source account, destination account, amount, fee, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)