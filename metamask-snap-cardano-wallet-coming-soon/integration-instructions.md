# Integration instructions

Integrates your dApp with the `Cardano Wallet` Metamask [snap](https://metamask.io/snaps/). This means that in order to log into your dApp, it is enough for the user to have Metamask installed, removing the need for having a Cardano-specific wallet set up.

## Demo

Example dApp with the current version of SDK is deployed [here](https://sdk-example.nu.fi/).

Example integration can be found in [https://github.com/nufi-official/adaplays.xyz](https://github.com/nufi-official/adaplays.xyz) which is a forked/updated version of playground Cardano dApp.

We recommend checking usage of `@nufi/dapp-client-core` and `@nufi/dapp-client-cardano` in the [File](https://github.com/nufi-official/adaplays.xyz/blob/main/components/navbar.tsx) where most of the changes are contained. Alternatively just searching for the usage of these libraries should showcase all relevant steps in the integration.

The other changes made to this repository are specific to its example dApp, so we do not recommend focusing on them.

## Install custom Metamask Flask

_Note that the custom Metamask Flask has to be used due to changes in the Metamask extension itself, that were not yet published to production_.

Download the Metamask Flask extension from [here](https://github.com/nufi-official/metamask-extension/releases/tag/v11.10.0-flask-cip3-allow-remote-snap) or click [here](https://github.com/nufi-official/metamask-extension/releases/download/v11.10.0-flask-cip3-allow-remote-snap/v11.10.0-flask-cip3-allow-remote-snap.zip) to download it directly.

Once downloaded:

* Extract the attached zip file
* Use a separate Chrome profile to not mess with the production Metamask extension
* Navigate to `chrome://extensions/`
* Press "Load unpacked"
* Choose the "chrome" folder of the extracted zip file
* Alternatively, use "firefox" folder if using Firefox

## Install packages

NPM

```
npm install @nufi/dapp-client-core
npm install @nufi/dapp-client-cardano
```

Yarn

```
yarn add @nufi/dapp-client-core
yarn add @nufi/dapp-client-cardano
```

## Usage

### Initialize core SDK

The guide below explains how to set up MetaMask Snap Cardano Wallet in a mainnet or testnet staging environment. When you are ready to run this service in a production environment, please [contact us](https://nufi.gitbook.io/developer-docs/nuficonnect-dapp-sdk-for-cardano/get-help) so that we can whitelist your domain(s) and enable the service to use a production version of NuFi wallet.

```
import nufiCoreSdk from '@nufi/dapp-client-core'

// preprod network (runs against staging version of NuFi)
nufiCoreSdk.init('https://wallet-testnet-staging.nu.fi')

// OR

// preview network (runs against staging version of NuFi)
nufiCoreSdk.init('https://wallet-preview-staging.nu.fi')

// OR

// mainnet network (runs against staging version of NuFi)
nufiCoreSdk.init('https://wallet-staging.nu.fi')
```

The `init` function has to be called before calling other functions from `@nufi/dapp-client-core` or `@nufi/dapp-client-cardano` SDK.

Its advisable to call it as soon as possible as it will also prefetch the Widget, and will make it appear faster when being requested later on.

If no origin is passed to `init` it defaults to `https://wallet.nu.fi`. Note that this default will not work until officially released.

For now please use the origin from the above example.

### Check whether the user has Metamask installed

```
import nufiCoreSdk from '@nufi/dapp-client-core'

nufiCoreSdk.getApi().isMetamaskInstalled().then((isMetamaskInstalled) => {
  // `isMetamaskInstalled` is `true` if user has Metamask installed
  // You can e.g. set your local state to reflect that and display
  // login with metamask option.
})
```

### Initialize Snap login for Cardano

```
import nufiCoreSdk from '@nufi/dapp-client-core'
import {initNufiDappCardanoSdk} from '@nufi/dapp-client-cardano'

// Should be called before accessing `window.cardano.nufiSnap`
initNufiDappCardanoSdk(nufiCoreSdk, 'snap')
const api = await window.cardano.nufiSnap.enable()
```

The `initNufiDappCardanoSdk` will populate `window.cardano.nufiSnap` object which has methods corresponding to the CIP-30 standard.

See [multiple providers docs](https://github.com/nufi-official/nufi-dapp-sdk/blob/main/docs/multipleProviders.md) to use `initNufiDappCardanoSdk` correctly, when supporting multiple providers.

### HideWidget

```
import nufiCoreSdk from '@nufi/dapp-client-core'

nufiCoreSdk.getApi().hideWidget()
```

Use this method to close the Widget in case the user logs out using your dApp.

### Show widget

When calling CIP-30 `enable` method the Widget will be shown automatically.

userTherefore if you detect (possibly a flag in your localStorage) that user is logged in you can simply call the `enable` method to make the Widget visible.

### Selecting Extension provider

For users with NuFi extension installed, there are no specific actions required. Simply access `window.cardano.nufi` from anywhere as it is not controlled by the NuFi Widget SDK.

## Limitations



* The terms and conditions will be updated before going to production.
