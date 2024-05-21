# Integration instructions

## Demo

An example dApp with the current version of SDK is deployed [here](https://sdk-example.nu.fi/).

Example integration can be found in [https://github.com/nufi-official/adaplays.xyz](https://github.com/nufi-official/adaplays.xyz) which is a forked/updated version of playground cardano dApp.

We recommend checking usage of `@nufi/dapp-client-core`, `@nufi/dapp-client-cardano` and `@nufi/sso-button-react` in [File 1](https://github.com/nufi-official/adaplays.xyz/blob/main/components/navbar.tsx) and [File 2](https://github.com/nufi-official/adaplays.xyz/blob/main/pages/\_app.tsx) where most of the changes are contained. Alternatively just searching for the usage of these libraries should showcase all relevant steps in the integration.

The other changes made to this repository are specific to its example dApp, so we do not recommend focusing on them.

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

The guide below explains how to set up NuFiConnect in a mainnet or testnet staging environment. When you are ready to run this service in a production environment, please [contact us](https://nufi.gitbook.io/developer-docs/nuficonnect-dapp-sdk-for-cardano/get-help) so that we can whitelist your domain(s) and enable the service to use a production version of NuFi wallet.

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

If no origin is passed to `init` it defaults to `https://wallet.nu.fi`. Note that this default will not work until it is officially released.

For now please use the origin from the above example.

### Initialize SSO login for Cardano

```
import nufiCoreSdk from '@nufi/dapp-client-core'
import {initNufiDappCardanoSdk} from '@nufi/dapp-client-cardano'

// Should be called before accessing `window.cardano.nufiSSO`
initNufiDappCardanoSdk(nufiCoreSdk, 'sso')
const api = await window.cardano.nufiSSO.enable()
```

When called like in the example above users will be asked to choose the Web3Auth provider inside the NuFi Widget. If you want to choose a specific provider you can pass it using `provider` parameter like this:

```
import nufiCoreSdk from '@nufi/dapp-client-core'
import {initNufiDappCardanoSdk} from '@nufi/dapp-client-cardano'

// Should be called before accessing `window.cardano.nufiSSO`
initNufiDappCardanoSdk(nufiCoreSdk, 'sso', {provider: 'google'})
const api = await window.cardano.nufiSSO.enable()
```

You can currently choose `google` and `discord` providers.

The `initNufiDappCardanoSdk` will populate `window.cardano.nufiSSO` object which has methods corresponding to the CIP-30 standard.

See [multiple providers docs](https://github.com/nufi-official/nufi-dapp-sdk/blob/main/docs/multipleProviders.md) to use `initNufiDappCardanoSdk` correctly, when supporting multiple providers.

### Listening to social login info changes

You can listen to the changes of current social login info using the following:

```
import nufiCoreSdk from '@nufi/dapp-client-core'

const currentSSOInfo = nufiCoreSdk.getApi().onSocialLoginInfoChanged((data) => {
  // Store data in your app
})
```

Alternatively, you can call:

```
import nufiCoreSdk from '@nufi/dapp-client-core'

const currentSSOInfo = nufiCoreSdk.getApi().getSocialLoginInfo()
```

The returned data is either `null` or of the following type

```
export type SocialLoginInfo = {
  email: string | null
  name: string | null
  profileImage: string | null
  typeOfLogin: 'google' | 'discord'
} & Record<string, unknown>
```

### HideWidget

```
import nufiCoreSdk from '@nufi/dapp-client-core'

nufiCoreSdk.getApi().hideWidget()
```

Use this method to close the Widget in case user logs out using your dapp.

### Show widget

When calling CIP-30 `enable` method the Widget will be shown automatically.

Therefore if you detect (possibly a flag in your localStorage) that users is logged in you can simply call the `enable` method to make the Widget visible.

### Use SsoButton for React

You can use the `@nufi/dapp-client-core` and `@nufi/dapp-client-cardano` with any JS framework, though in case you are using React we prepared a simple Social login button widget that you can use out of the box.

You can always use the SDK with you custom Button widget.

NPM

```
npm install @nufi/sso-button-react
```

Yarn

```
yarn add @nufi/sso-button-react
```

```
import nufiCoreSdk from '@nufi/dapp-client-core'
import {initNufiDappCardanoSdk} from '@nufi/dapp-client-cardano'
import {SsoButton} from '@nufi/sso-button-react'
import '@nufi/sso-button-react/dist/style.css'

// Logged in example
<SsoButton
  state="logged_in"
  label={ssoUserInfo?.email || 'Connected'}
  userInfo={{
    provider: ssoUserInfo?.typeOfLogin
  }}
  isLoading={isDisconnecting}
  onLogout={() => {
    // custom logic
  }}
  classes={{
    base: styles.yourCustomClass
  }}
/>
```

```
import nufiCoreSdk from '@nufi/dapp-client-core'
import {initNufiDappCardanoSdk} from '@nufi/dapp-client-cardano'
import {SsoButton} from '@nufi/sso-button-react'
import '@nufi/sso-button-react/dist/style.css'

// Logged out example
<SsoButton
  state="logged_out"
  label="Social login"
  isLoading={isConnecting}
  onLogin={() => {
    // custom logic
    initNufiDappCardanoSdk(nufiCoreSdk, 'sso');
    // custom logic
  }}
  classes={{
    base: styles.yourCustomClassName
  }}
/>
```

For a complete example please check [here](https://github.com/nufi-official/adaplays.xyz/commit/641466c4e8b534f1461692cac6987396b77b5c7c).

### Selecting Extension provider

For users with NuFi extension installed, there are no specific actions required. Simply access `window.cardano.nufi` from anywhere as it is not controlled by the NuFi Widget SDK.

## Limitations

* The terms and conditions will be updated before going to production.
