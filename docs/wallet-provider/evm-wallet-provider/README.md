# EVM Wallet Provider

## What is EVM Wallet Provider

The EVM Wallet Provider Submodule submodule helps you create wallets locally for EVM (Ethereum Virtual Machine) blockchains.The submodule comes with simple functions to create special phrases called mnemonics, extended public keys (xpubs), private keys, and addresses, as well as to handle transactions on EVM blockchains.

## Get Started Using

To get started using EVM Wallet Providers, you would need to install @tatumio/evm-wallet-provider along with the Tatum SDK.

{% tabs %}
{% tab title="Typescript/Javascript SDK" %}
```bash
npm install @tatumio/evm-wallet-provider
```
{% endtab %}
{% endtabs %}

## What are the use cases EVM Wallet Provider Submodule helps with?&#x20;

1. Mnemonic Generation: Generate mnemonics for seed phrases effortlessly, a foundational step for wallet creation and management.&#x20;
2. Extended Public Key (xpub) Creation: Create xpubs from mnemonics seamlessly, paving the way for deriving addresses and managing wallets.&#x20;
3. Private Key and Address Derivation: Derive private keys and addresses from mnemonics and xpubs efficiently, ensuring secure and organized wallet management.&#x20;
4. Transaction Signing and Broadcasting: Sign and broadcast transactions to EVM-based networks with ease, facilitating smooth interactions with the blockchain.&#x20;
5. Cross-Blockchain Development: With support for a multitude of EVM-based networks, extend your development horizons across various blockchain platforms including Ethereum, Binance Smart Chain, Polygon, and more. Secure dApp Development:

The EVM Wallet Provider submodule is an indispensable companion for developers striving to excel in the EVM blockchain ecosystem. Its extensive functionalities make it a reliable and potent toolkit for advanced wallet management and blockchain interaction.

## Supported Chains

<table><thead><tr><th width="180">Blockchain</th><th width="264">Mainnet</th><th>Testnet</th></tr></thead><tbody><tr><td>Arbitrum</td><td>Network.ARBITRUM_NOVA<br><br>Network.ARBITRUM_ONE</td><td>Network.ARBITRUM_NOVA_TESTNET</td></tr><tr><td>Aurora</td><td>Network.AURORA</td><td>Network.AURORA_TESTNET</td></tr><tr><td>Avalanche</td><td>Network.AVALANCHE_C</td><td>Network.AVALANCHE_C_TESTNET</td></tr><tr><td>Binance Smart Chain</td><td>Network.BINANCE_SMART_CHAIN</td><td>Network.BINANCE_SMART_CHAIN_TESTNET</td></tr><tr><td>Celo</td><td>Network.CELO</td><td>Network.CELO_ALFAJORES</td></tr><tr><td>Chilliz</td><td>Network.CHILIZ</td><td></td></tr><tr><td>Cronos</td><td>Network.CRONOS</td><td>Network.CRONOS_TESTNET</td></tr><tr><td>Ethereum</td><td>Network.ETHEREUM</td><td>Network.ETHEREUM_SEPOLIA<br>Network.ETHEREUM_GOERLI</td></tr><tr><td>Ethereum Classic</td><td>Network.ETHEREUM_CLASSIC</td><td></td></tr><tr><td>Fantom</td><td>Network.FANTOM</td><td>Network.FANTOM_TESTNET</td></tr><tr><td>Flare</td><td>Network.FLARE</td><td>Network.FLARE_COSTON<br>Network.FLARE_COSTON_2<br>Network.FLARE_SONGBIRD</td></tr><tr><td>Gnosis</td><td>Network.GNOSIS</td><td>Network.GNOSIS_TESTNET</td></tr><tr><td>Harmony</td><td>Network.HARMONY_ONE_SHARD_0</td><td>Network.HARMONY_ONE_TESTNET_SHARD_0</td></tr><tr><td>Haqq</td><td>Network.HAQQ</td><td>Network.HAQQ_TESTNET</td></tr><tr><td>Horizen</td><td>Network.HORIZEN_EON</td><td>Network.HORIZEN_EON_GOBI</td></tr><tr><td>Klaytn</td><td>Network.KLAYTN</td><td>Network.KLAYTN_BAOBAB</td></tr><tr><td>KuCoin</td><td>Network.KUCOIN</td><td>Network.KUCOIN_TESTNET</td></tr><tr><td>Oasis</td><td>Network.OASIS</td><td>Network.OASIS_TESTNET</td></tr><tr><td>Optimism</td><td>Network.OPTIMISM</td><td>Network.OPTIMISM_TESTNET</td></tr><tr><td>Palm</td><td>Network.PALM</td><td>Network.PALM_TESTNET</td></tr><tr><td>Polygon</td><td>Network.POLYGON</td><td>Network.POLYGON_MUMBAI</td></tr><tr><td>VeChain</td><td>Network.VECHAIN</td><td>Network.VECHAIN_TESTNET</td></tr><tr><td>XDC</td><td>Network.XDC</td><td>Network.XDC_TESTNET</td></tr></tbody></table>

###
