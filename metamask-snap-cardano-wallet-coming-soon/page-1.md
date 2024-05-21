# Overview

## Introduction

#### _This service is coming soon_

MetaMask Snap for Cardano (or ‘Snap’ for short) is a service that makes Cardano DApps instantly accessible to MetaMask’s millions of users. It adds MetaMask wallet support to a Cardano DApp so that MetaMask users can connect to a Cardano DApp using only their MetaMask wallet.

With Snap, a MetaMask user can start using a Cardano DApp in under 10 seconds. They navigate to a DApp that’s using the Snap service, and click ‘Connect with MetaMask’; in the background, the service creates a non-custodial Cardano wallet for the user and connects the user to the DApp automatically.

The Cardano wallet created invisibly for the user is non-custodial and its credentials are derived from the user’s MetaMask wallet credentials. This is possible thanks to MetaMask’s new Snaps technology, whose goal is to extend MetaMask’s functionality to non-EVM chains like Cardano.

After connecting to a DApp, a MetaMask user can access their Cardano wallet using a wallet widget in the corner of the screen. Through this widget, a user can approve or reject transactions, manage assets (including NFTs), purchase ADA with fiat, swap Cardano tokens using a DEX aggregator (powered by DexHunter), and exchange 500+ assets for ADA using a cross-chain exchange.

## Wallet functionality

Snap creates a non-custodial Cardano wallet for the user in the background and connects the user’s wallet to the DApp automatically. This wallet is embedded into the DApp itself and is accessible from a wallet widget in the corner of the DApp.

Using the wallet widget, a user can approve transactions (the widget pops up automatically when there's an action to be taken) and is able to manage assets including NFTs.

This wallet widget also includes a `BUY ADA` button that opens a fiat on-ramp (for the user to buy ADA with a card, Apple/Google pay, etc) and a button to swap tokens, which directs the user to the Cardano DEX aggregator, where the user can acquire any Cardano token they need.

There’s also a cross-chain exchange available to the user which supports 500+ crypto assets (and doesn’t require a user to sign up or KYC in order to use it). With this exchange, a user can swap e.g. ETH or stablecoins (in any wallet) for ADA and deposit directly into their Snap wallet.

## Security

Snap is a non-custodial service composed of various non-custodial, open-source, and audited components.

MetaMask Snap for Cardano is a key component of the service. It derives a Cardano wallet private key based on the user’s MetaMask wallet’s credentials. The technology used to do this is open-source and audited.

The user's Cardano wallet private key is injected into a non-custodial Cardano wallet (a lite version of NuFi); the Snap service then shares the wallet’s public key with the DApp in order to connect the user.

Important to know: the user’s private key never leaves the user's device and is never shared with the DApp.

When the user performs a transaction, they first view and approve it inside the Snap wallet widget (which launches automatically when there’s an action for the user to take). After the transaction is approved in the wallet widget, MetaMask wallet launches and prompts the user to approve the transaction in MetaMask’s interface too. If approved in MetaMask, the transaction is submitted on the Cardano blockchain by the Snap service.

### Seed phrase backup

Users can easily export their seed phrase from Metamask and store it securely.

\


\
