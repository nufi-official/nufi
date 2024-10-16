# Overview

## Introduction

Thanks to [Snaps](https://snaps.metamask.io/), the Cardano ecosystem is directly accessible to MetaMask’s millions of users. Using the Cardano Wallet Snap, users can interact with Cardano dApps directly through their MetaMask.

With the Cardano Wallet Snap, a MetaMask user can start using a Cardano DApp in under 10 seconds. Here’s how it works:

1. The user navigates to a Cardano DApp and selects MetaMask from the wallet options.

<figure><img src="../.gitbook/assets/gitbook edited (1).png" alt="" width="305"><figcaption></figcaption></figure>

1. The user is prompted to install Cardano Wallet Snap in their MetaMask wallet.

![](https://lh7-us.googleusercontent.com/docsz/AD\_4nXfSWgU9ms0qqN\_JLt3mRPynFr53MCvIG3U7JGdgNgvJhbW4hpqciV80wrCwpM90VoeOCCTnFP4o-SI347jkLVlEDiGhgOf\_1d43yGultDb-JXFg6AS1exV4vm6qpDXdGMlCyTLx3WlkzA74g45p\_A9qBiSr?key=XnlM6nH3wkXg7Jpid9qweQ)

3. The user’s MetaMask Cardano wallet – created for them behind the scenes instantly – is successfully connected to the DApp.



{% embed url="https://www.youtube.com/watch?v=lL1xx9Q6nCE" %}

## How it works

The MetaMask Cardano Wallet consists of two main components:

1. **Cardano Wallet Snap**\
   A MetaMask Snap that enables the user’s MetaMask wallet to derive Cardano keys and sign Cardano transactions. The Snap is installed by the user and runs directly in the MetaMask browser extension wallet. When asked to sign a transaction, the Snap triggers a MetaMask popup, and the user must confirm the action in the MetaMask wallet.
2. **NuFi Widget**\
   The NuFi widget is a DApp-integrated wallet UI that provides complete wallet functionalities such as managing and sending Cardano assets, including NFTs, purchasing ADA with a credit card, cross-chain exchange, and a Cardano DEX aggregator. The widget is integrated into the DApp via SDK and serves as a user-friendly layer between the MetaMask and the DApp.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

For additional functionalities like staking, detailed portfolio overview, sending multiple tokens, and more, users can simply open the NuFi dashboard. It can be accessed directly from the widget or via [wallet.nu.fi](http://wallet.nu.fi).

<figure><img src="../.gitbook/assets/chrome-extension___gpnihlnnodeiiaakbikldcihojploeca_index.html(1920) (85).png" alt=""><figcaption></figcaption></figure>

In a common scenario, a sign transaction request from a DApp is sent to the NuFi widget, which shows transaction details and prompts the user to confirm. If the user confirms, the NuFi widget asks MetaMask to sign the transaction. MetaMask displays a popup, and if the user confirms, it signs the transaction.



{% embed url="https://www.youtube.com/watch?v=x-wlkQCdQSs" %}

## Wallet functionality

NuFi’s service provides Cardano wallet functionality for a MetaMask user while they’re connected to a DApp.&#x20;

The user’s Cardano wallet is embedded into the DApp itself and is accessible from a widget located in the corner of the DApp. Using the wallet widget, a user can approve transactions (the widget pops up automatically when there's an action to be taken) and can manage assets including NFTs.&#x20;

This wallet widget includes a BUY ADA button that opens a fiat on-ramp (for the user to buy ADA with the card, Apple/Google pay, etc) and a button to Exchange tokens, which directs the user to cross-chain Exchange (to swap 500+ tokens for ADA) and to a Cardano DEX aggregator (powered by DexHunter), where the user can acquire any Cardano token they need.

## Security

Cardano Wallet Snap provides MetaMask with the capability to derive Cardano keys and sign Cardano transactions using these keys. The Snap is open-source and [audited](https://sayfer.io/audits/metamask-snap-audit-report-for-nufi/).

The NuFi widget is a bridge between a Cardano DApp and MetaMask. When the user initiates a transaction, they first review and approve the transaction inside the NuFi widget. After the transaction is approved in the widget, the MetaMask wallet launches and prompts the user to approve and sign the transaction in MetaMask’s interface. If approved in MetaMask, the signed transaction is returned to NuFi widget and submitted on the Cardano blockchain.

Important to know: the private key is never shared with the DApp or NuFi widget. The derivation of the private key and transaction signing always happens in the MetaMask core.

### Seed phrase backup

The Cardano Wallet keys are derived directly from the MetaMask seed phrase. Users can easily export their MetaMask seed phrase and import it into any other Cardano wallet that supports a 12-word phrase.

## Partners

\
MetaMask Snap Cardano Wallet is used by [DexHunter](https://app.dexhunter.io/), [WingRiders](https://app.wingriders.com/), [VyF](http://vyfi.io/)i, [GeniusYield](https://www.geniusyield.co/), [Jam on Bread](http://jamonbread.io/), [WayUp](http://wayup.io/), [Cardano Crypto Casino](https://cardanocryptocasino.com/), [Cardano Casino](https://cardanocasino.vip/), [Coinecta](https://coinecta.fi/), [FluidTokens](https://fluidtokens.com/), Anvil, [Axo](https://www.axo.trade/), Mesh, [Ada Markets](https://ada.markets/), [Levvy](https://levvy.fi/) and [Crashr](https://www.crashr.io/).
