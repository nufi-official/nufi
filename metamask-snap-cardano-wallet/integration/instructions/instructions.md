<img src="./images/cardano_metamask.svg" alt="drawing" width="200"/>

# Integration instructions

Integrates your DApp with the `Cardano Wallet` Metamask [snap](https://metamask.io/snaps/). This means that in order to log into your DApp, it is enough for the user to have Metamask installed, removing the need for having a Cardano-specific wallet set up.

## Demo

Example dapp with the current version of SDK is deployed [here](https://sdk-example.nu.fi/).

Example integration can be found in [https://github.com/nufi-official/adaplays.xyz](https://github.com/nufi-official/adaplays.xyz) which is a forked/updated version of playground cardano dapp.

We recommend to check usage of `@nufi/dapp-client-core` and `@nufi/dapp-client-cardano` in [File](https://github.com/nufi-official/adaplays.xyz/blob/main/components/navbar.tsx) where most of the changes are contained. Alternatively just searching for the usage of these libraries should showcase all relevant steps in the integration.

The other changes made to this repository are specific to its example dapp, so we do not recommend focusing on them.

## Migration

If migrating from older version of SDK please take a look at [_migration docs_](../common/migrations.md).

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

// mainnet network
nufiCoreSdk.init('https://wallet.nu.fi')

// OR

// preprod network (runs against staging version of NuFi)
nufiCoreSdk.init('https://wallet-testnet-staging.nu.fi')

// OR

// preview network (runs against staging version of NuFi)
nufiCoreSdk.init('https://wallet-preview-staging.nu.fi')
```

The `init` function has to be called before calling other functions from `@nufi/dapp-client-core` or `@nufi/dapp-client-cardano` SDK.

Its advisable to call it as soon as possible as it will also prefetch the Widget, and will make it appear faster when being requested later on.

If no origin is passed to `init` it defaults to `https://wallet.nu.fi`. Note that this default will not work until officially released.

For now please use the origin from the above example.

To customize Widget appearance (such as z-index, color mode, featured tokens, manual expand or collapse), please see [Widget options](../common/widgetOptions.md)

### Check whether user has Metamask installed

Note that the Widget handles cases when users do not have Metamask installed. Therefore its fine to always show some "Login with MetaMask" button on your dapp.

If you nevertheless wish to detect whether the MetaMask is installed, you can do it via the following call:

```
import nufiCoreSdk from '@nufi/dapp-client-core'

nufiCoreSdk.isMetamaskInstalled().then((isMetamaskInstalled) => {
  // `isMetamaskInstalled` is `true` if user has Metamask installed
  // You can e.g. set your local state to reflect that and display
  // login with metamask option.
})
```

#### Known limitations

On Firefox, the `nufiCoreSdk.isMetamaskInstalled()` method may always return `false` regardless of whether Metamask is installed or not. This is only relevant for dapps that use `script-src 'self'` as part of their Context Security Policy.
For these cases we suggest to always provide users with the Metamask login option,
as the NuFi Widget can handle Metamask detection correctly. Otherwise you can check specifically
for Firefox by using:

```
function isFirefox() {
  return (
    document.documentElement !== undefined &&
    'MozAppearance' in document?.documentElement?.style
  )
}
```

or a similar code.

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

const widgetApi = await nufiCoreSdk.getWidgetApi()
widgetApi.hideWidget()
```

Use this method to close the Widget in case user logs out using your dapp.

### Show widget

When calling CIP-30 `enable` method the Widget will be shown automatically.

Therefore if you detect (possibly a flag in your localStorage) that users is logged in you can simply call the `enable` method to make the Widget visible.

### Selecting Extension provider

For users with NuFi extension installed, there are no specific actions required. Simply access `window.cardano.nufi` from anywhere as it is not controlled by the NuFi Widget SDK.

### Note on Cardano Collaterals

If your Cardano DApp calls [getCollateral()](https://github.com/cardano-foundation/CIPs/blob/1006fed85a8346bff49aa10431ecf21e70dd4556/CIP-0030/README.md?plain=1#L282), for best UX please make sure to do so only when really needed, otherwise users may get needlessly prompted by the NuFi widget to set up a collateral even if they don't have to. Even better would be to use [CIP-40](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0040) which lets you use regular inputs as collateral, i.e. removes the need to request collateral explicitly from the wallet.

## Icon

As an icon for Metamask provider in your dapp, you can download this [svg](./images/cardano_metamask.svg).
