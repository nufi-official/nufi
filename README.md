<p align="center">
  <img src="https://user-images.githubusercontent.com/4980147/195955040-181cffc8-8a98-490c-b01d-0c9c8497734a.svg" /></p>
  <p align="center">
    A Web3 crypto wallet for Cardano, Flow and Solana.
    <br />
    <a href="https://chrome.google.com/webstore/detail/nufi/gpnihlnnodeiiaakbikldcihojploeca"><strong>Download extension</strong></a>
    <br />
    <a href="https://nu.fi/"><strong>Visit web app</strong></a>
  </p>
</p>

This repository provides technical information relevant especially for Dapp developers wanting to integrate with NuFi.

## Testnet extension

NuFi extension/web currently doesn't allow switching between mainnet/testnet. The extension available on Chrome webstore is mainnet. To test your dapp on testnet, you can download the latest testnet build of the extension [here](https://assets.nu.fi/extension/testnet/nufi-cwe-testnet-latest.zip)

## Dapp connectors

NuFi offers several Dapp connectors allowing it to interact with Dapps across multiple blockchains. Below are instructions/resources clarifying how to integrate them.

### Cardano

NuFi's Cardano connector implements the [CIP-30](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0030) standard and the API should behave the same as Flint wallet's CIP-30 connector, except it's injected as `window.cardano.nufi`. More info at https://www.cardano-caniuse.io

### Solana

NuFi's Solana connector can be integrated through the official solana-labs [wallet-adapter library](https://github.com/solana-labs/wallet-adapter/tree/master/packages/wallets/nufi). The interface should be a clone of Phantom wallet.

### Flow

NuFi works with the official [fcl-js](https://github.com/onflow/fcl-js) SDK and is fully integrated with the [fcl-discovery](https://github.com/onflow/fcl-discovery) service. If you want to integrate NuFi directly, the parameters needed for that can be found [here](https://github.com/onflow/fcl-discovery/blob/812bff5b90343976835d17bc2d7810aac62d714d/data/services.json#L74). 
