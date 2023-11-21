# getAccountBalance

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, CardanoRosetta, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Cardano
const tatum = await TatumSDK.init<CardanoRosetta>({ network: Network.CARDANO_ROSETTA });

// Define the input parameters in a single object
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
            chain_code: 'CHAIN_CODE', // Specify chain code only if applicable
        },
    },
    blockIdentifier: {
        index: 1123941,  // number (int64), optional
        hash: '0x1f2cc6c5027d2f201a5453ad1119574d2aed23a392654742ac3c78783c071f85',  // string, optional
    }, // `blockIdentifier` is optional object
    currency: {
        symbol: 'ADA', // string, required
        decimals: 6,   // number, required
        metadata: {
            // Specify metadata if applicable
        },
    }, // `currency` is optional object
};

// Retrieve the account balance for the specified Cardano account
const accountBalance = await tatum.rpc.getAccountBalance(params);

// Log the account balance
console.log('Cardano Account Balance:', accountBalance);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccountBalance` method allows you to get an account's balance for a specified Cardano account identifier and block identifier.

### Example Use Cases

1. **Balance Summary**: Developers can use this method to retrieve the balance summary of a Cardano account, including the total balance and balances of specific sub-accounts.

### Request Parameters

The `getAccountBalance` method requires the following parameters:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to `'CARDANO'` for Cardano.
  - `network` (string, required): The network name for Cardano.
- `accountIdentifier` (object, optional): An object containing information about the account.
    - `address` (string, required): The Cardano account address associated with the operation.
    - `sub_account` (object, optional): An optional sub-account object.
      - `address` (string, optional): The sub-account address.
      - `metadata` (object, optional): An optional metadata object for the sub-account. If the SubAccount address is not sufficient to uniquely specify a SubAccount, any other identifying information can be stored here. It is important to note that two SubAccounts with identical addresses but differing metadata will not be considered equal by clients.
    - `metadata` (object, optional): An optional metadata object for the account. Blockchains that utilize a username model (where the address is not a derivative of a cryptographic public key) should specify the public key(s) owned by the address in metadata.
- `blockIdentifier` (object, optional): An object containing information about the block.
  - `index` (number, optional): The index of the block (Type: number, Format: int64).
  - `hash` (string, optional): The hash of the block.
- `currency` (object, required): An object specifying the currency details.
    - `symbol` (string, required): The symbol or code of the currency.
    - `decimals` (number, required): The number of decimal places for the currency.
    - `metadata` (object, optional): Any additional information related to the currency itself. For example, it would be useful to populate this object with the contract address of an ERC-20 token.

### Return Object

The method returns an object representing the account's balance for the specified Cardano account identifier and block identifier. It includes the total balance and balances of specific sub-accounts.

Structure and behavior of this method may vary with different versions of the Cardano service. Always refer to the documentation specific to the version you are using for the most accurate information.