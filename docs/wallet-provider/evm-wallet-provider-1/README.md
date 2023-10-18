# UTXO Wallet Provider

### Description

UTXO Wallet Provider extends wallet capabilities for UTXO-based blockchains via Tatum SDK, facilitating:

* Mnemonic generation for seed phrases.
* xpub creation from mnemonics.
* Private key and address derivation from mnemonics and xpubs.
* Transaction signing and broadcasting to UTXO networks.

Utilizes well-regarded packages like bitcoinjs-lib, bitcore-lib, bip39, and bip32.

### Quick Start

#### Installation

```bash
npm install @tatumio/utxo-wallet-provider
```

```javascript
import { UtxoWalletProvider } from '@tatumio/utxo-wallet-provider';

const tatumSdk = await TatumSDK.init<Bitcoin>({
     network: Network.BITCOIN,
     configureWalletProviders: [
         UtxoWalletProvider,
     ]
 });
```

### Supported Networks

* Network.BITCOIN
* Network.DOGECOIN
* Network.LITECOIN
* Network.BITCOIN\_TESTNET
* Network.DOGECOIN\_TESTNET
* Network.LITECOIN\_TESTNET

Remember to keep mnemonics, private keys, and other sensitive data secure. Avoid exposing them in client-side code or public repositories.
