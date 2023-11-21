# searchTransactions

### How to Use

```typescript
import { TatumSDK, CardanoRosetta, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Cardano
const tatum = await TatumSDK.init<CardanoRosetta>({ network: Network.CARDANO_ROSETTA });

// Define the input parameters in a single object
const params = {
    networkIdentifier: {
        blockchain: 'CARDANO',
        network: 'NETWORK_NAME',
        subNetworkIdentifier: {
            network: 'SUB_NETWORK_NAME',
            metadata: {
                // Optional metadata key-value pairs.
            },
        },
    },
    operator: {
        // Specify search conditions (optional).
    },
    max_block: 5,   // The largest block index to consider (optional).
    offset: 5,      // The offset into the query result to start returning transactions (optional).
    limit: 5,       // The maximum number of transactions to return in one call (optional).
    transactionIdentifier: {
        hash: 'TRANSACTION_HASH',  // string, required
    },
    accountIdentifier: {
        address: 'ACCOUNT_ADDRESS', // string, required
        sub_account: {
            // Specify sub-account information if applicable
        },
        metadata: {
            chain_code: 'CHAIN_CODE', // Specify chain code if applicable
        },
    },
    coin_identifier: {
        identifier: 'CO' // Specify search conditions (optional).
    },
    currency: {
            symbol: 'CURRENCY_SYMBOL', // Required: Specifies the currency symbol .
            decimals: 6, // Required: Specifies the currency decimals (number).
            metadata: {
              // Optional metadata for amount object
            },
    },
    status: 'reverted', // The network-specific operation status type (optional).
    type: 'transfer',   // The network-specific operation type (optional).
    address: '0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347', // Account address (optional).
    success: true,  // A synthetic condition (optional).
};

// Search for transactions
const transactions = await tatum.rpc.searchTransactions(params);

// Log the retrieved transactions
console.log('Transactions:', transactions);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `searchTransactions` method allows you to search for transactions matching a set of provided conditions in canonical blocks. This can be useful for querying transaction data based on various criteria.

### Example Use Cases

1. **Transaction Query**: Developers can use this method to search for transactions that meet specific criteria, such as a particular status or operation type.
2. **Block Analysis**: Users can analyze transactions within a specific range of blocks to identify patterns or trends.

## Request Parameters

The `searchTransactions` method requires the following parameters in the request body:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to `CARDANO` for Cardano.
  - `network` (string, required): The network name for Cardano.
  - `subNetworkIdentifier` (object, optional): An optional sub-network identifier object.
    - `network` (string, optional): The name of the sub-network within Cardano.
    - `metadata` (object, optional): Metadata associated with the sub-network.
- `operator` (enum, optional): Additional search conditions `or` and `and`.
- `max_block` (number, optional): The largest block index to consider when searching for transactions. If not populated, the current block is considered the `max_block`. If you do not specify a `max_block`, it is possible that a newly synced block will interfere with paginated transaction queries (as the offset could become invalid with newly added rows).
- `offset` (number, optional): The offset into the query result to start returning transactions. If any search conditions are changed, the query offset will change, and you must restart your search iteration.
- `limit` (number, optional): The maximum number of transactions to return in one call. The implementation may return <= `limit` transactions.
- `transactionIdentifier` (object, required): An object containing information about the transaction.
  - `hash` (string, required): The hash of the transaction.
- `accountIdentifier` (object, optional): An object containing information about the account.
    - `address` (string, required): The Cardano account address associated with the operation.
    - `sub_account` (object, optional): An optional sub-account object.
        - `address` (string, optional): The sub-account address.
        - `metadata` (object, optional): An optional metadata object for the sub-account. If the SubAccount address is not sufficient to uniquely specify a SubAccount, any other identifying information can be stored here. It is important to note that two SubAccounts with identical addresses but differing metadata will not be considered equal by clients.
    - `metadata` (object, optional): An optional metadata object for the account.
- `coinIdentifier` (object, optional): Specify search conditions for coin identifier. Identifier should be populated with a globally unique identifier of a Coin. In Bitcoin, this identifier would be transaction_hash: index.
    - `identifier` (string, required): Example: '0x2f23fd8cca835af21f3ac375bac601f97ead75f2e79143bdf71fe2c4be043e8f: 1'
- `currency` (object, required): An object specifying the currency details.
      - `symbol` (string, required): The symbol or code of the currency.
      - `decimals` (number, required): The number of decimal places for the currency.
      - `metadata` (object, optional): Any additional information related to the currency itself. For example, it would be useful to populate this object with the contract address of an ERC-20 token.
- `status` (string, optional): The network-specific operation status type (optional).
- `type` (string, optional): The network-specific operation type (optional).
- `address` (string, optional): AccountIdentifier.Address. This is used to get all transactions related to an AccountIdentifier.Address, regardless of SubAccountIdentifier.
- `success` (boolean, optional): A synthetic condition populated by parsing network-specific operation statuses.

### Return Object

The method returns a list of transactions that match the specified search criteria.