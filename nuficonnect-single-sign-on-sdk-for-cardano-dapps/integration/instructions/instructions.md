# Integration instructions

Integrates your DApp with the NuFi web wallet injected into it is as a widget. Users can seamlessly onboard/log in into your DApp using social providers such as Google or Discord while being able to manage their wallet in the NuFi interface.

## Demo

Example dapp with the current version of SDK is deployed [here](https://sdk-example.nu.fi/).

Example integration can be found in [https://github.com/nufi-official/adaplays.xyz](https://github.com/nufi-official/adaplays.xyz) which is a forked/updated version of playground cardano dapp.

We recommend to check usage of `@nufi/dapp-client-core`, `@nufi/dapp-client-cardano` and `@nufi/sso-button-react` in [File 1](https://github.com/nufi-official/adaplays.xyz/blob/main/components/navbar.tsx) and [File 2](https://github.com/nufi-official/adaplays.xyz/blob/main/pages/_app.tsx) where most of the changes are contained. Alternatively just searching for the usage of these libraries should showcase all relevant steps in the integration.

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

// mainnet network
nufiCoreSdk.init('https://wallet.nu.fi')

// OR

// preprod network
nufiCoreSdk.init('https://wallet-testnet.nu.fi')

// OR

// preview network (runs against staging version of NuFi)
nufiCoreSdk.init('https://wallet-preview-staging.nu.fi')
```

The `init` function has to be called before calling other functions from `@nufi/dapp-client-core` or `@nufi/dapp-client-cardano` SDK.

Its advisable to call it as soon as possible as it will also prefetch the Widget, and will make it appear faster when being requested later on.

If no origin is passed to `init` it defaults to `https://wallet.nu.fi`.

To customize Widget appearance (such as z-index), please see [Widget options](../common/widgetOptions.md)

### Initialize SSO login for Cardano

```
import nufiCoreSdk from '@nufi/dapp-client-core'
import {initNufiDappCardanoSdk} from '@nufi/dapp-client-cardano'

// Should be called before accessing `window.cardano.nufiSSO`
initNufiDappCardanoSdk(nufiCoreSdk, 'sso')
const api = await window.cardano.nufiSSO.enable()
```

When called like in the example above users will be asked to choose Web3Auth provider inside the NuFi Widget. If you want to choose specific provider you can pass it using `provider` parameter like this:

```
import nufiCoreSdk from '@nufi/dapp-client-core'
import {initNufiDappCardanoSdk} from '@nufi/dapp-client-cardano'

// Should be called before accessing `window.cardano.nufiSSO`
initNufiDappCardanoSdk(nufiCoreSdk, 'sso', {provider: 'google'})
const api = await window.cardano.nufiSSO.enable()
```

You can currently choose `google` and `discord` providers.

The `initNufiDappCardanoSdk` will populate `window.cardano.nufiSSO` object which has methods corresponding to CIP-30 standard.

See [multiple providers docs](../common/multipleProviders.md) to use `initNufiDappCardanoSdk` correctly, when supporting multiple providers.

### Listening to social login info changes

You can listen to the changes of current social login info using the following:

```
import nufiCoreSdk from '@nufi/dapp-client-core'

const currentSSOInfo = nufiCoreSdk.getApi().onSocialLoginInfoChanged((data) => {
  // Store data in your app
})
```

Alternatively you can call:

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

You can find the assets for the Login button [here](https://github.com/nufi-official/nufi-dapp-sdk/tree/main/packages/sso-button-react/src/assets).

#### Button position

For seamless user navigation, it is recommended that the Login button be positioned in the top bar, to the left of the Wallet selection options.

<figure><img src="./images/button-position-1.png" alt=""><figcaption><p>Recommended button position</p></figcaption></figure>

If the DApp UI does not allow this, the Login button can be placed inside the Wallet selection options as the top option.

<figure><img src="./images/button-position-2.png" alt="" width="375"><figcaption><p>Login button inside Wallet options</p></figcaption></figure>

\

### Selecting Extension provider

For users with NuFi extension installed, there are no specific actions required. Simply access `window.cardano.nufi` from anywhere as it is not controlled by the NuFi Widget SDK.

### Note on Cardano Collaterals

If your Cardano DApp calls [getCollateral()](https://github.com/cardano-foundation/CIPs/blob/1006fed85a8346bff49aa10431ecf21e70dd4556/CIP-0030/README.md?plain=1#L282), for best UX please make sure to do so only when really needed, otherwise users may get needlessly prompted by the NuFi widget to set up a collateral even if they don't have to. Even better would be to use [CIP-40](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0040) which lets you use regular inputs as collateral, i.e. removes the need to request collateral explicitly from the wallet.

## Whitelist

### NuFiConnect mainnet

To integrate the widget on mainnet, your DApp's domain needs need to be whitelisted. Please [contact us](../common/contact.md) and specify the domains to be whitelisted.

Note that `localhost` with any port is supported by default.

### On-off ramp service

If you want a service user to be able to purchase crypto inside the widget using a fiat on-ramp (powered by Moonpay), your DApp's domain needs to be whitelisted. Please [contact us](../common/contact.md) and specify the domains to be whitelisted.

Once whitelisted you will need to use [this extension](https://chromewebstore.google.com/detail/always-disable-content-se/ffelghdomoehpceihalcnbmnodohkibj) for local testing, or ensure that your dapp is locally accessible via `http://localhost` or `https://localhost` (i.e. no port number in the URL).
