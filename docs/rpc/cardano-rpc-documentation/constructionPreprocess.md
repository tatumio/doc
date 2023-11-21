# constructionPreprocess

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, CardanoRosetta, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Cardano
const tatum = await TatumSDK.init<CardanoRosetta>({ network: Network.CARDANO_ROSETTA });

// Define the input parameters in a single object
const params = {
    networkIdentifier: {
      blockchain: 'CARDANO', // Required: Specifies the blockchain .
      network: 'MAINNET', // Required: Specifies the network name .
      subNetworkIdentifier: {
        network: 'SUB_NETWORK_NAME', // Optional: Specifies the sub-network name .
        metadata: {
          KEY: 'VALUE', // Optional: Specify metadata .
        },
      },
    },
    operations: [
      {
        operation_identifier: {
          index: 1, // Required: Specifies the operation index (number).
          network_index: 0, // Optional: Specifies the network index (number).
        },
        related_operations: [
          {
            index: 2, // Optional: Specifies the related operation index (number).
            network_index: 1, // Optional: Specifies the related network index (number).
          },
        ],
        type: 'OPERATION_TYPE', // Required: Specifies the operation type.
        status: 'OPERATION_STATUS', // Optional: Specifies the operation status .
        account: {
          address: 'ACCOUNT_ADDRESS', // Required: Specifies the account address .
          sub_account: {
            address: 'SUB_ACCOUNT_ADDRESS', // Optional: Specifies the sub-account address .
            metadata: {
              // Optional metadata object for the sub-account
            },
          },
          metadata: {
            // Optional metadata object for the account
          },
        },
        amount: {
          value: 'AMOUNT_VALUE', // Required: Specifies the amount value (string).
          currency: {
            symbol: 'CURRENCY_SYMBOL', // Required: Specifies the currency symbol .
            decimals: 6, // Required: Specifies the currency decimals (number).
            metadata: {
              // Optional metadata for amount object
            },
          },
          metadata: {
            // Optional: Specify metadata here only if applicable.
          },
        },
        coin_change: {
          coin_identifier: {
            identifier: 'COIN_IDENTIFIER', // Required: uniquely identifies a Coin.
          },
          coin_action: 'coin_created', // Required
        },
        metadata: {
          // Optional: Specify operations metadata only if applicable.
        }
      },
    ],
    metadata: {
      //Optional: Specify constructionPreprocess metadata only if applicable.
    }
};

// Create a request to fetch metadata for transaction construction
const preprocessRequest = await tatum.rpc.constructionPreprocess(params);

// Log the preprocess request
console.log('Construction Preprocess Request:', preprocessRequest);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `constructionPreprocess` method is called prior to `constructionPayloads` to construct a request for any metadata that is needed for transaction construction. This method is used to fetch information such as account nonce. The `options` object returned from this method will be sent to the `constructionMetadata` endpoint **UNMODIFIED** by the caller in an offline execution environment. If your Construction API implementation has configuration options, they MUST be specified in the `constructionPreprocess` request in the `metadata` field.

### Example Use Cases

1. **Transaction Construction**: Developers can use this method to fetch metadata required for transaction construction, such as the account nonce.
2. **Validation**: Validators can use this method to validate transaction data before the actual transaction construction.

### Request Parameters

The `constructionPreprocess` method requires the following parameters:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to `CARDANO` for Cardano.
  - `network` (string, required): The network name for Cardano.
  - `subNetworkIdentifier` (object, optional): An optional sub-network identifier object.
    - `network` (string, required): The name of the sub-network within Cardano.
    - `metadata` (object, optional): Metadata associated with the sub-network.
- `operations` (array of objects, required): An array of operation objects, where each object represents a transaction to be included in the Cardano transaction.
  - `operation_identifier` (object, required): An object containing an index that uniquely identifies the operation.
    - `index` (number, required): The index of the operation.
    - `network_index` (number, optional): The network-specific index of the operation.
  - `related_operations` (array of objects, optional): An array of related operation identifiers if applicable.
    - `index` (number, optional): The index of the related operation.
    - `network_index` (number, optional): The network-specific index of the related operation.
  - `type` (string, required): The type of the operation (e.g., "TRANSFER").
  - `status` (string, optional): The status of the operation (e.g., "SUCCESS").
  - `account` (object, required): An object containing information about the account.
    - `address` (string, required): The Cardano account address associated with the operation.
    - `sub_account` (object, optional): An optional sub-account object.
      - `address` (string, optional): The sub-account address.
      - `metadata` (object, optional): An optional metadata object for the sub-account. If the SubAccount address is not sufficient to uniquely specify a SubAccount, any other identifying information can be stored here. It is important to note that two SubAccounts with identical addresses but differing metadata will not be considered equal by clients.
    - `metadata` (object, optional): An optional metadata object for the account. Blockchains that utilize a username model (where the address is not a derivative of a cryptographic public key) should specify the public key(s) owned by the address in metadata.
  - `amount` (object, required): An object containing information about the transaction amount.
    - `value` (string, required): The value of the transaction amount.
    - `currency` (object, required): An object specifying the currency details.
      - `symbol` (string, required): The symbol or code of the currency.
      - `decimals` (number, required): The number of decimal places for the currency.
      - `metadata` (object, optional): Any additional information related to the currency itself. For example, it would be useful to populate this object with the contract address of an ERC-20 token.
    - `metadata` (object, optional): metadata object for the amount.
  - `coin_change` (object, required): An object containing information about coin changes in the operation.
    - `coin_identifier` (object, required): An object containing a coin identifier.
      - `identifier` (string, required): Identifier should be populated with a globally unique identifier of a Coin. In Bitcoin, this identifier would be transaction_hash:index..
    - `coin_action` (string, required): CoinActions are different state changes that a Coin can undergo. When a Coin is created, it is coin_created. When a Coin is spent, it is coin_spent. It is assumed that a single Coin cannot be created or spent more than once. (e.g., 'coin_created' | 'coin_spent').
  - `metadata` (object, optional): An optional metadata object for the operation, including withdrawal, deposit, refund, staking credential, pool key hash, epoch, token bundle, pool registration certificate, pool registration parameters, and vote registration metadata details.
- `metadata` (object, optional): Metadata for `constructionPreprocess`

### Return Object

The method returns an object representing the preprocess request for transaction construction. This object includes the metadata required for constructing the transaction. The `options` object in this request will be sent to the `constructionMetadata` endpoint **UNMODIFIED** by the caller in an offline execution environment. 

Structure and behavior of this method may vary with different versions of the Cardano service. Always refer to the documentation specific to the version you are using for the most accurate information.