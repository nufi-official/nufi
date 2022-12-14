<p align="center">
  <img src="https://user-images.githubusercontent.com/4980147/196724563-43b703ed-461e-4759-9e09-12f023debfa3.png" /></p>
  <p align="center">
    <i>A Web3 crypto wallet for Cardano, Ethereum, Flow and Solana.</i>
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

## DApp connectors

NuFi offers several DApp connectors allowing it to interact with DApps across multiple blockchains. Below are instructions/resources clarifying how to integrate them.

### Cardano

NuFi's Cardano connector implements the [CIP-30](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0030) standard and the API should behave the same as Flint wallet's CIP-30 connector, except it's injected as `window.cardano.nufi`. More info at https://www.cardano-caniuse.io

### Ethereum

NuFi's Ethereum connector implements Metamask's API documented here: https://docs.metamask.io/guide/ethereum-provider.html#methods with the exception of account/network switching during the connection, which at the moment isn't supported by NuFi. Note that NuFi will not inject its API if it detects Metamask or other wallet injecting into the `window.ethereum` object, to avoid interference with these wallets. Therefore, in order to use NuFi's Ethereum connector you need to make sure that there are no other active ethereum wallet extensions (i.e. they must be disabled/uninstalled). 

### Solana

NuFi's Solana connector can be integrated through the official solana-labs [wallet-adapter library](https://github.com/solana-labs/wallet-adapter/tree/master/packages/wallets/nufi). The interface should be a clone of Phantom wallet.

### Flow

NuFi works with the official [fcl-js](https://github.com/onflow/fcl-js) SDK and is fully integrated with the [fcl-discovery](https://github.com/onflow/fcl-discovery) service. If you want to integrate NuFi directly, the parameters needed for that can be found [here](https://github.com/onflow/fcl-discovery/blob/812bff5b90343976835d17bc2d7810aac62d714d/data/services.json#L74).

## Branding guidelines

Download [here](https://assets.nu.fi/brand.zip)

## Support

You can contact us by creating a new support ticket [here](https://support.nu.fi/support/tickets/new)


