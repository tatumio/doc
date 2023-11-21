# getAccountCoins

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, CardanoRosetta, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Cardano
const tatum = await TatumSDK.init<CardanoRosetta>({ network: Network.CARDANO_ROSETTA });

// Define the input parameter in a single object
const params = {
    networkIdentifier: {
        blockchain: 'CARDANO',  // string, required
        network: 'NETWORK_NAME',  // string, required
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
    includeMempool: true, // boolean, optional
    currency: {
        symbol: 'ADA', // string, required
        decimals: 6,   // number, required
        metadata: {
            // Specify metadata only if applicable
        },
    },
};

// Retrieve unspent coins for an account in Cardano blockchain
const unspentCoins = await tatum.rpc.getAccountCoins(params);

// Log the unspent coins
console.log('Unspent Coins:', unspentCoins);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccountCoins` method allows you to get an array of all unspent coins for a Cardano account.

### Example Use Cases

1. **Account Balance**: Developers can use this method to retrieve the unspent coins for a Cardano account and calculate its balance.

### Request Parameters

The `getAccountCoins` method requires the following parameters:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to `'CARDANO'` for Cardano.
  - `network` (string, required): The network name for Cardano.
- `accountIdentifier` (object, optional): An object containing information about the account.
    - `address` (string, required): The Cardano account address associated with the operation.
    - `sub_account` (object, optional): An optional sub-account object.
      - `address` (string, optional): The sub-account address.
      - `metadata` (object, optional): An optional metadata object for the sub-account. If the SubAccount address is not sufficient to uniquely specify a SubAccount, any other identifying information can be stored here. It is important to note that two SubAccounts with identical addresses but differing metadata will not be considered equal by clients.
    - `metadata` (object, optional): An optional metadata object for the account. Blockchains that utilize a username model (where the address is not a derivative of a cryptographic public key) should specify the public key(s) owned by the address in metadata.
- `includeMempool` (boolean, optional): An optional boolean flag to indicate whether to include mempool transactions. Default is `true`.
- `currency` (object, required): An object specifying the currency details.
    - `symbol` (string, required): The symbol or code of the currency.
    - `decimals` (number, required): The number of decimal places for the currency.
    - `metadata` (object, optional): Any additional information related to the currency itself. For example, it would be useful to populate this object with the contract address of an ERC-20 token.

### Return Object

The method returns an object representing the unspent coins for the specified Cardano account. This object includes details about the unspent coins and the block identifier at which the lookup was performed.

Please note that the structure of the returned object may vary based on the Cardano RPC version.