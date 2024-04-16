# DApp connector

### DApp connectors

NuFi offers several DApp connectors allowing it to interact with DApps across multiple blockchains. Below are instructions/resources clarifying how to integrate them.

#### Cardano

NuFi's Cardano connector implements the [CIP-30](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0030) standard and the API should behave the same as Flint wallet's CIP-30 connector, except it's injected as `window.cardano.nufi`. More info at https://www.cardano-caniuse.io

#### Ethereum / Milkomeda C1 / Polygon

NuFi's Ethereum connector implements Metamask's API documented here: https://docs.metamask.io/guide/ethereum-provider.html#methods. When integrating NuFi we suggest following the [eip-5749](https://eips.ethereum.org/EIPS/eip-5749) standard and load NuFi from `window.evmproviders`.

**Legacy `window.ethereum` injection**

NuFi still offers legacy support and also tries to inject itself into`window.ethereum,` but we discourage using this approach and rather move to eip-5749 proposal. Note that in that case, NuFi will not inject its API if it detects Metamask or other wallet injecting into the `window.ethereum` object, to avoid interference with these wallets. Therefore, in order to use NuFi's Ethereum connector you need to make sure that there are no other active Ethereum wallet extensions (i.e. they must be disabled/uninstalled).

EVM chains currently supported by NuFi's connector:

* Ethereum
* Milkomeda C1
* Polygon

#### Solana

NuFi's Solana connector can be integrated through the Solana Wallet Standard ([https://github.com/anza-xyz/wallet-standard](https://github.com/anza-xyz/wallet-standard)).

#### Flow

NuFi works with the official [fcl-js](https://github.com/onflow/fcl-js) SDK and is fully integrated with the [fcl-discovery](https://github.com/onflow/fcl-discovery) service. If you want to integrate NuFi directly, the parameters needed for that can be found [here](https://github.com/onflow/fcl-discovery/blob/812bff5b90343976835d17bc2d7810aac62d714d/data/services.json#L74).
