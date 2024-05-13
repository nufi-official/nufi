# Overview

## Introduction

NuFiConnect is a service for Cardano dApps that enables Web2 (non-crypto) users to connect to a dApp without needing a wallet.

To do this, NuFiConnect adds social account login options to a dApp’s frontend; when a Web2 user logs in with a social account Google, Facebook, X, and so on, NuFiConnect creates a non-custodial Cardano wallet for the user in the background and connects the user to the dApp automatically.

During onboarding, a Web2 user doesn’t need to download or set up anything and doesn’t need to write down a seed phrase. Onboarding takes less than 10 seconds for new users.

After connecting to a dApp, a Web2 user can access their non-custodial Cardano wallet using a wallet widget in the corner of the screen. Through this widget, a user can approve or reject transactions, manage assets (including NFTs), purchase ADA with fiat, and swap Cardano tokens using a DEX aggregator (powered by DexHunter).

## NuFiConnect Vs. Existing services

Existing social account login (i.e. Single Sign-On, SSO) services do not allow a Web2 user to re-use the same wallet across multiple dApps, even if the user logs in with the same social account.

The result is that a Web2 user has a different wallet for each dApp they log in to (which is confusing and inconvenient).

NuFiConnect fixes this problem so that a Web2 user can re-use the same SSO wallet across all dApps that use our service.

This is very important if, for example, a Web2 user acquires an NFT on one site (e.g. on a secondary NFT marketplace or a minting dApp) and wants to use it in a different place (e.g. a Web3 game or another dApp).

This isn't possible with existing services because they don't allow wallets/assets to be re-used across multiple dApps. NuFiConnect, on the other hand, allows a Web2 user to re-use the same wallet across all dApps that use the service.

On top of that, the NuFiConnect service provides Cardano wallet functionality for a Web2 user so a dApp doesn't need to integrate and maintain wallet functionality themselves.

## Wallet functionality

NuFiConnect creates a non-custodial Cardano wallet for the user in the background. This wallet is embedded into the dApp itself and is accessible from a wallet widget in the corner of the dApp.

Using the wallet widget, a user can approve transactions (the widget pops up automatically when there's an action to be taken) and can manage assets including NFTs.

This wallet widget includes a `BUY ADA` button that opens a fiat on-ramp (for the user to buy ADA with the card, Apple/Google pay, etc) and a button to swap tokens, which directs the user to Cardano DEX aggregator (powered by DexHunter), where the user can acquire any Cardano token they need.

The wallet widget’s appearance and behavior can be customized by a project. We’re also able to provide a fully customized integration if a project requires it (which allows for, among other things, custom buttons and functionality).

## Security

NuFiConnect is a non-custodial service composed of several non-custodial components.

Web3Auth's walletless onboarding stack is used for social account login functionality and authentication, as well as to handle decentralized private key management.

This last one is a mechanism for securely storing and retrieving wallet credentials with no central authority. It "leverages the security, immutability, availability, and resiliency properties of distributed ledgers to provide highly scalable key distribution, verification, and recovery."

In a nutshell, the user's private key is sharded (i.e. broken into bits) and stored securely by nodes of a decentralized network (whose operators include Binance, Tendermint, ENS, and other crypto industry behemoths).

When the Web2 user logs in to a social account, the private key shards are fetched to the user's device and — only on the device — get re-assembled into a complete private key, which is injected into a non-custodial wallet. This is the Web2 user's new Cardano wallet, created for them in seconds behind the scenes.

Our service then shares the user's public key with the dApp to connect the user.

Important to know: the complete private key never leaves the user's device and is never shared with the dApp.

\
\
\
