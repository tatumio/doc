---
description: >-
  Transaction Simulator integrates seamlessly with Tatum SDK to provide
  transaction simulation capabilities for EVM-based blockchains.
---

# 🧾 Transaction Simulator

### 📖 Description <a href="#user-content--description" id="user-content--description"></a>

The Transaction Simulator is designed to bolster the efficiency and security of blockchain transactions. It offers crucial capabilities such as:

* Simulating native currency transfers.
* Simulating ERC20 token transfers.

By leveraging these simulations, developers can:

1. **Estimate Fees Accurately:** One of the primary challenges in sending blockchain transactions is determining an optimal gas fee that ensures quick confirmation without overpaying. By simulating a transaction before sending it, developers can get a precise estimate of the gas fee, saving costs and improving user experience.
2. **Enhance Safety:** Simulating transactions allows developers to anticipate and catch potential errors or vulnerabilities in transaction logic. By identifying these issues in a simulation environment, developers can prevent costly mistakes when deploying actual transactions.
3. **Optimize Transaction Parameters:** Beyond just estimating fees, simulating transactions can help developers fine-tune other parameters, such as gas limit or nonce, to optimize transaction performance.

It is built upon popular packages like `ethers`, ensuring a robust, reliable, and secure foundation for all simulation activities.

### 🚀 Quick Start <a href="#user-content--quick-start" id="user-content--quick-start"></a>

1.  **Installation**

    Firstly, ensure that the `@tatumio/transaction-simulator` package is set as a dependency within your project. Next, import the Transaction Simulator extension:

    ```
    import { TransactionSimulator } from '@tatumio/transaction-simulator';
    ```
2.  **Initialization**

    Create an instance of Tatum SDK passing `TransactionSimulator` as one of extensions.

    ```
    const tatumSdk = await TatumSDK.init<Ethereum>({
         network: Network.ETHEREUM,
         configureExtensions: [
             TransactionSimulator,
         ]
     })
    ```

### 🛠️ ERC20 Token Transfers: <a href="#user-content-how-to-use" id="user-content-how-to-use"></a>

1.  **Define Your Token Transfer Payload**: To simulate an ERC20 token transfer, you will use the `TokenTransfer` object.

    ```
    const tokenTransferPayload: TokenTransfer = {
      to: 'recipient_address',
      from: 'sender_address',
      gas: '0xB411', // optional
      gasPrice: '0x4B16C370A', //optional
      value: 500, // example token amount to send
      tokenContractAddress: 'your_erc20_token_contract_address'
    };
    ```
2.  **Call `simulateTransferErc20`**: With your `TokenTransfer` payload ready, pass it to the `simulateTransferErc20` method.

    ```
    const tokenSimulationResult = await simulateTransferErc20(tokenTransferPayload);
    ```

    This method fetches token details, simulates the transaction, and returns an estimation of the transaction's outcome along with the necessary gas fees.
3.  **Check simulation results**:

    ```
    {
      "transactionDetails": {
        "from": "0xDce92f40cAdDE2C4e3EA78b8892c540e6bFe2f81",
        "to": "0xaf758da9f7bdaa7590175193388e9c99427cc2d2",
        "tokenContractAddress": "0xdac17f958d2ee523a2206206994597c13d831ec7",
        "data": "0xa9059cbb000000000000000000000000af758da9f7bdaa7590175193388e9c99427cc2d2000000000000000000000000000000000000000000000000000000001908b100",
        "gasLimit": 46097,
        "gasPrice": 20156528394
      },
      "status": "success",
      "balanceChanges": {
        "0xDce92f40cAdDE2C4e3EA78b8892c540e6bFe2f81": {
          "from": 243656557299636170000,
          "to": 243655628144146780000
        }
      },
      "tokenTransfers": {
        "0xdac17f958d2ee523a2206206994597c13d831ec7": {
          "name": "TetherUSD",
          "symbol": "USDT",
          "decimals": 6,
          "0xDce92f40cAdDE2C4e3EA78b8892c540e6bFe2f81": {
            "from": 2387468.080258,
            "to": 2387048.080258
          },
          "0xaf758da9f7bdaa7590175193388e9c99427cc2d2": {
            "from": 422.304,
            "to": 842.304
          }
        }
      }
    }
    ```

By using the above methods, you can efficiently predict the behavior and costs of your transactions before actually broadcasting them, ensuring optimized and error-free transactions.

## Gas Price Estimation: <a href="#user-content-gas-price-estimation" id="user-content-gas-price-estimation"></a>

* Methods accept `gasPrice` as a parameter. If you don't provide it, the gas price will be estimated using the `eth_gasPrice` method.
* Methods accept `gas` as a parameter. If you don't provide it, the gas limit will be estimated using the `eth_estimateGas` method.

### 🔗🔗 Supported Networks <a href="#user-content--supported-networks" id="user-content--supported-networks"></a>

```
Network.ETHEREUM,
Network.ETHEREUM_SEPOLIA,
Network.ETHEREUM_CLASSIC,
Network.ETHEREUM_GOERLI,
Network.ETHEREUM_HOLESKY,
Network.AVALANCHE_C,
Network.AVALANCHE_C_TESTNET,
Network.POLYGON,
Network.POLYGON_MUMBAI,
Network.GNOSIS,
Network.GNOSIS_TESTNET,
Network.FANTOM,
Network.FANTOM_TESTNET,
Network.AURORA,
Network.AURORA_TESTNET,
Network.CELO,
Network.CELO_ALFAJORES,
Network.BINANCE_SMART_CHAIN_TESTNET,
Network.VECHAIN,
Network.VECHAIN_TESTNET,
Network.XDC,
Network.XDC_TESTNET,
Network.PALM,
Network.PALM_TESTNET,
Network.CRONOS,
Network.CRONOS_TESTNET,
Network.KUCOIN,
Network.KUCOIN_TESTNET,
Network.OASIS,
Network.OASIS_TESTNET,
Network.OPTIMISM,
Network.OPTIMISM_TESTNET,
Network.HARMONY_ONE_SHARD_0,
Network.HARMONY_ONE_TESTNET_SHARD_0,
Network.KLAYTN,
Network.KLAYTN_BAOBAB,
Network.FLARE_COSTON,
Network.FLARE_COSTON_2,
Network.FLARE,
Network.FLARE_SONGBIRD,
Network.HAQQ,
Network.HAQQ_TESTNET,
Network.ARBITRUM_NOVA,
Network.ARBITRUM_NOVA_TESTNET,
Network.ARBITRUM_ONE,
Network.BINANCE_SMART_CHAIN,
Network.HORIZEN_EON,
Network.HORIZEN_EON_GOBI,
Network.CHILIZ
```
