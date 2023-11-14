# getConractTickets

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the contract ID
const params = { 
    contractId: 'YOUR_CONTRACT_ID',
    chainId: 'YOUR_CHAIN_ID',           // Specify the chain ID (Network identifier)
    blockId: 'YOUR_BLOCK_ID',            // Optional: Specify the block ID if needed
};

// Retrieve all ticket balances for a specific Tezos smart contract
const ticketBalances = await tatum.rpc.getConractTickets(params);

// Log the ticket balances
console.log(`All Ticket Balances for Contract ${contractId}:`, ticketBalances);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getConractTickets` method is used to retrieve the balances of all tickets associated with a specific Tezos smart contract. Tickets represent assets or tokens held within a smart contract, and this method provides information about those assets' balances.

### Example Use Cases:

1. **Asset Management:** Developers and users can use this method to query the balances of all tickets held within a Tezos smart contract. This is particularly useful for asset management and tracking within decentralized applications.

2. **Audit and Verification:** Auditors and verifiers can check the ticket balances within a smart contract to ensure that the contract behaves as expected and that all assets are accounted for.

### Request Parameters

The `getConractTickets` method requires the following parameter:

- `contractId` (string, required): The contract ID (address) of the Tezos smart contract for which you want to retrieve the ticket balances.
- `chainId` (string, required): The ID of the chain where the block is located.
- `blockId` (string, required): The unique identifier (hash) of the block.

### Return Object

The method returns an array of objects, each representing a ticket balance within the specified Tezos smart contract. Each object includes the following properties:

- `ticketer` (string): The ticketer associated with the ticket balance.

- `content_type` (string): The content type of the ticket.

- `content` (string): The content associated with the ticket.

- `amount` (string): The amount or balance of the ticket.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)