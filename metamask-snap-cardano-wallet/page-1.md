# Overview

## Introduction

**This service is coming soon**

MetaMask Cardano Wallet Snap  (or ‘Snap’ for short) is a service that makes Cardano DApps instantly accessible to MetaMask’s millions of users. It adds Cardano support to MetaMask so that MetaMask users can connect to a Cardano DApp using only their MetaMask wallet. This is possible thanks to [MetaMask Snaps](https://metamask.io/snaps/) technology, whose goal is to extend MetaMask’s functionality to non-EVM chains like Cardano.

With Snap, a MetaMask user can start using a Cardano DApp in under 10 seconds. They navigate to a Cardano DApp that has a NuFi Widget for Cardano Wallet Snap integrated, and click ‘Connect with MetaMask’; the user will be prompted to enable Cardano Wallet Snap in their MetaMask which will instantly derive Cardano wallet keys from the MetaMask seed phrase.

After connecting to a DApp, a MetaMask user can see their MetaMask Cardano wallet balance in the NuFi widget in the corner of the screen. Through this widget, a user can review transaction details (before confirming and signing in their MetaMask wallet), manage assets including NFTs, purchase ADA with a credit card, swap Cardano tokens using a DEX aggregator (powered by DexHunter), and exchange 500+ assets for ADA using a cross-chain exchange.

The private key to the Cardano Wallet never leaves MetaMask! It is never exposed to the dApp or to the Cardano Wallet Snap.

## How it works

The Metamask Cardano Wallet service consists of two main components.&#x20;

1. Cardano Wallet Snap

A Metamask snap, that enables the user’s Metamask wallet to expose methods for deriving Cardano keys and signing Cardano transactions. The snap has to be installed by the user and runs directly in the Metamask wallet. When asked to sign a transaction the snap triggers a Metamask popup and the user has to confirm the action in the Metamask wallet. Cardano Wallet snap serves as a bridge between Metamask wallet and NuFi widget.

2. NuFi Widget

Facilitates a non-custodial Cardano Wallet from the user’s Metamask Wallet seed phrase. It does so, by asking for public keys and transaction signatures from Cardano Wallet snap. This way it serves as a bridge between a Cardano Wallet snap and a Cardano Dapp. It is integrated into the Dapp and comes with an integrated wallet UI that provides wallet functionalities such as sending, trading, staking, and more.

In a common scenario, a sign transaction request from a Dapp is sent to the NuFi widget, which shows transaction details and prompts the user to confirm. If the user confirms, the NuFi widget asks the Metamask wallet to sign the transaction. Metamask wallet displays a popup and if the user confirms, it signs the transaction using Cardano Wallet snap.

## Wallet functionality

Cardano Wallet Snap creates a non-custodial Cardano wallet for the user in the background and connects the user’s wallet to the DApp automatically. The Snap is communicating with the DApp via the NuFi widget which can be accessed in the bottom left corner of the screen.

Using the NuFi widget, a user can review transactions (the widget pops up automatically when there's an action to be taken) and is able to manage assets including NFTs.

This wallet widget also includes a BUY ADA button that opens a fiat on-ramp (for the user to buy ADA with a card, Apple/Google pay, etc) and a button to swap tokens, which directs the user to a Cardano DEX aggregator, where the user can acquire any Cardano token they need.

There’s also a cross-chain exchange available to the user which supports 500+ crypto assets (and doesn’t require a user to sign up or KYC in order to use it). With this exchange, a user can swap e.g. ETH or stablecoins (in any wallet) for ADA.

A MetaMask user can also access their Cardano account by visiting [wallet.nu.fi](http://wallet.nu.fi) and clicking the MetaMask icon. This will open the user’s Cardano account inside NuFi wallet dashboard, where the user can access additional functionality such as ADA staking and a detailed portfolio overview.

## Security

Cardano Wallet for MetaMask is a non-custodial service composed of various non-custodial, open-source, and audited components.

Cardano Wallet Snap is a key component of the service. It provides MetaMask with the capability to derive Cardano keys and sign Cardano transactions using these keys. The Snap is open-source and audited.

NuFi widget is a bridge between a DApp and Cardano Wallet Snap. When the user performs a transaction, they first review and approve the transaction inside the NuFi widget (which launches automatically when there’s an action for the user to take). After the transaction is approved in the widget, MetaMask wallet launches and prompts the user to approve and sign the transaction in MetaMask’s interface. If approved in MetaMask, the transaction is submitted on the Cardano blockchain by NuFi widget.

Important to know: the private key is never shared with the Snap, Widget or DApp. The derivation of the private key and transaction signing happens always in the MetaMask core.

### Seed phrase backup

A user can restore their Cardano account in a non-custodial Cardano wallet using their MetaMask wallet’s seed phrase.
