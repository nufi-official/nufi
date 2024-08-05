<img src="./images/cardano_metamask.svg" alt="drawing" width="200"/>

# Integration instructions 

Integrates your DApp with the `Cardano Wallet` Metamask [snap](https://metamask.io/snaps/). This means that in order to log into your DApp, it is enough for the user to have Metamask installed, removing the need for having a Cardano-specific wallet set up.

## Demo

Example dapp with the current version of SDK is deployed [here](https://sdk-example.nu.fi/).

Example integration can be found in [https://github.com/nufi-official/adaplays.xyz](https://github.com/nufi-official/adaplays.xyz) which is a forked/updated version of playground cardano dapp.

We recommend to check usage of `@nufi/dapp-client-core` and `@nufi/dapp-client-cardano` in [File](https://github.com/nufi-official/adaplays.xyz/blob/main/components/navbar.tsx) where most of the changes are contained. Alternatively just searching for the usage of these libraries should showcase all relevant steps in the integration.

The other changes made to this repository are specific to its example dapp, so we do not recommend focusing on them.

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

_Make sure that your app's Content Security Policy does not block the iframe that is injected by our SDK. For more info please check_ [_iframe injection docs_](../common/iframeInjection.md)_._

### Initialize core SDK

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

To customize Widget appearance (such as z-index), please see [Widget options](../common/widgetOptions.md)

### Check whether user has Metamask installed

Note that the Widget handles cases when users do not have Metamask installed. Therefore its fine to always show some "Login with MetaMask" button on your dapp.

If you nevertheless wish to detect whether the MetaMask is installed, you can do it via the following call:

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

The `initNufiDappCardanoSdk` will populate `window.cardano.nufiSnap` object which has methods corresponding to CIP-30 standard.

See [multiple providers docs](../common/multipleProviders.md) to use `initNufiDappCardanoSdk` correctly, when supporting multiple providers.

### HideWidget

```
import nufiCoreSdk from '@nufi/dapp-client-core'

nufiCoreSdk.getApi().hideWidget()
```

Use this method to close the Widget in case user logs out using your dapp.

### Show widget

When calling CIP-30 `enable` method the Widget will be shown automatically.

Therefore if you detect (possibly a flag in your localStorage) that users is logged in you can simply call the `enable` method to make the Widget visible.

### Selecting Extension provider

For users with NuFi extension installed, there are no specific actions required. Simply access `window.cardano.nufi` from anywhere as it is not controlled by the NuFi Widget SDK.

### Note on Cardano Collaterals

If your Cardano DApp calls [getCollateral()](https://github.com/cardano-foundation/CIPs/blob/1006fed85a8346bff49aa10431ecf21e70dd4556/CIP-0030/README.md?plain=1#L282), for best UX please make sure to do so only when really needed, otherwise users may get needlessly prompted by the NuFi widget to set up a collateral even if they don't have to. Even better would be to use [CIP-40](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0040) which lets you use regular inputs as collateral, i.e. removes the need to request collateral explicitly from the wallet.

## Whitelist

### On-off ramp service

If you want a service user to be able to purchase crypto inside the widget using a fiat on-ramp (powered by Moonpay), your DApp's domain needs to be whitelisted. Please [contact us](../common/contact.md) and specify the domains to be whitelisted.

Once whitelisted you will need to use [this extension](https://chromewebstore.google.com/detail/always-disable-content-se/ffelghdomoehpceihalcnbmnodohkibj) for local testing, or ensure that your dapp is locally accessible via `http://localhost` or `https://localhost` (i.e. no port number in the URL).

## Icon
As an icon for Metamask provider in your dapp, you can download this [svg](./images/cardano_metamask.svg).

## Limitations

- The terms and conditions will be updated before going to production.
