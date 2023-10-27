[![CircleCI](https://dl.circleci.com/status-badge/img/gh/vacuumlabs/nufi/tree/develop.svg?style=svg&circle-token=56c620137f72f17d4fd3370385e694f55d7170b6)](https://dl.circleci.com/status-badge/redirect/gh/vacuumlabs/nufi/tree/develop)

<p align="center">
  <img src="https://user-images.githubusercontent.com/4980147/196724563-43b703ed-461e-4759-9e09-12f023debfa3.png" /></p>
  <p align="center">
    <i>A Web3 crypto wallet for Cardano, Ethereum, Flow, Solana, Milkomeda C1 and Polygon.</i>
    <br />
    <br />
    <a href="https://chrome.google.com/webstore/detail/nufi/gpnihlnnodeiiaakbikldcihojploeca"><strong>Download extension</strong></a>
    ·
    <a href="https://nu.fi">Visit web</a>
    ·
    <a href="https://support.nu.fi/support/home">Knowledge base</a>

  </p>
</p>

This repository provides documentation/resources for DApp developers wanting to integrate with NuFi.

## Testnet extension

NuFi extension/web currently doesn't allow switching between mainnet/testnet. The extension available on Chrome webstore is configured for mainnet. To test your dapp on testnet, you can download the latest testnet build of the extension [here](https://assets.nu.fi/extension/testnet/nufi-cwe-testnet-latest.zip)

[Guide on how to install Chrome extension from .zip](https://bashvlas.com/blog/install-chrome-extension-in-developer-mode/)

### Cardano Sanchonet build

In order to test NuFi with the Cardano Conway-era testnet (Sanchonet) and [CIP-95](https://developers.cardano.org/docs/governance/cardano-improvement-proposals/cip-0095/), please download this [build](https://assets.nu.fi/extension/sanchonet/nufi-cwe-sanchonet-latest.zip) of the extension.

## DApp connectors

NuFi offers several DApp connectors allowing it to interact with DApps across multiple blockchains. Below are instructions/resources clarifying how to integrate them.

### Cardano

NuFi's Cardano connector implements the [CIP-30](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0030) standard and the API should behave the same as Flint wallet's CIP-30 connector, except it's injected as `window.cardano.nufi`. More info at https://www.cardano-caniuse.io

### Ethereum / Milkomeda C1 / Polygon

NuFi's Ethereum connector implements Metamask's API documented here: https://docs.metamask.io/guide/ethereum-provider.html#methods.
When integrating NuFi we suggest following the [eip-5749](https://eips.ethereum.org/EIPS/eip-5749) standard and load NuFi from `window.evmproviders`.

#### Legacy `window.ethereum` injection
NuFi still offers legacy support and also tries to inject itself into `window.ethereum`, but we discourage using this approach and rather move to eip-5749 proposal.
Note that in that case NuFi will not inject its API if it detects Metamask or other wallet injecting into the `window.ethereum` object, to avoid interference with these wallets. Therefore, in order to use NuFi's Ethereum connector you need to make sure that there are no other active ethereum wallet extensions (i.e. they must be disabled/uninstalled).

EVM chains currently supported by NuFi's connector:
* Etherem
* Milkomeda C1
* Polygon

### Solana

NuFi's Solana connector can be integrated through the official solana-labs [wallet-adapter library](https://github.com/solana-labs/wallet-adapter/tree/master/packages/wallets/nufi). The interface should be a clone of Phantom wallet.

### Flow

NuFi works with the official [fcl-js](https://github.com/onflow/fcl-js) SDK and is fully integrated with the [fcl-discovery](https://github.com/onflow/fcl-discovery) service. If you want to integrate NuFi directly, the parameters needed for that can be found [here](https://github.com/onflow/fcl-discovery/blob/812bff5b90343976835d17bc2d7810aac62d714d/data/services.json#L74).

## Branding guidelines

Download [here](https://assets.nu.fi/brand.zip)

## Support

You can contact us by creating a new support ticket [here](https://support.nu.fi/support/tickets/new)


