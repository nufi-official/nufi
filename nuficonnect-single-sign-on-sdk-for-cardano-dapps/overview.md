# Overview

## Introduction

#### _**This service is currently in Closed Beta phase**_

NuFiConnect is a service for Cardano dApps that enables Web2 (non-crypto) users to connect to a dApp without needing a wallet.

{% embed url="https://www.youtube.com/embed/7aOCLNwAZhQ?si=kXqp0chJfU2EEnrb" %}

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

### Two-Factor Authentication (2FA)

Unlike classic crypto wallets, NuFiConnect does not require you to store and memorize a seed phrase. Instead, we offer a secure and user-friendly experience without compromising security. All you need is access to your social account, so it’s crucial to keep those secure.

To enhance your security, we strongly recommend enabling Two-Factor Authentication (2FA) for the social account linked to your NuFiConnect.

**What is 2FA?**

2FA adds an extra layer of security by requiring a temporary code, in addition to your password, when there is an attempted login from an unrecognized device or browser.

**How to Set Up 2FA**

1. **Choose a 2FA App**: We recommend using apps like Google Authenticator.
2. **Enable 2FA**: Follow the instructions provided by your email or social account service to enable 2FA. This usually involves scanning a QR code with your 2FA app.
3. **Secure Your Phone**: Ensure that your phone, which will generate the 2FA codes, is also secure.

Enabling 2FA greatly enhances your security, making it almost impossible for unauthorized users to access your account without both your password and your phone. We encourage setting up 2FA on all your important platforms.

## FAQ

Q: Is NuFiConnect a non-custodial service?

A: Yes, all components of NuFiConnect are non-custodial.

Q: Does NuFiConnect replace existing wallet connection options?

A: No, NuFiConnect does not replace a dApp’s existing wallet connection options.

Q: Is it multi-chain?

A: At present, NuFiConnect runs on Cardano mainnet and Cardano preprod testnet, and there are plans to deploy NuFiConnect on other chains in the coming months.

Q: How can a Web2 user get ADA or Cardano tokens?

A: After a Web2 user has connected by logging in with a social account, the user can access a wallet widget in the corner of the dApp’s screen. Through this widget, a user can buy ADA with a credit card and swap Cardano tokens using a DEX aggregator powered by DexHunter.

Q: Where can I try this service?

A: You can try NuFiConnect [here](https://sdk-example.nu.fi/) using a testing DApp called Adaplays (please note that the password you enter is requested by the DApp and is not part of our service).

You can get tADA from the testnet faucet [here](https://docs.cardano.org/cardano-testnets/tools/faucet/) (be sure to select Preprod Testnet as the environment).\

\
\
\
