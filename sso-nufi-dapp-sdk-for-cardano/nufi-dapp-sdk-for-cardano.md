# NuFi dapp SDK for Cardano

## NuFi dapp SDK for Cardano

## Demo

Example dapp with the current version of SDK is deployed [here](https://sdk-example.nu.fi).

Snippets of example integration can be found [here](https://github.com/nufi-official/adaplays.xyz/commit/641466c4e8b534f1461692cac6987396b77b5c7c). Note that the versions in `package.json` need to be updated to the latest available.

### Install packages

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

### Usage

#### Initialize core SDK

```typescript
import nufiCoreSdk from '@nufi/dapp-client-core'
nufiCoreSdk.init('https://wallet-testnet-staging.nu.fi')
```

The `init` function has to be called before calling other functions from `@nufi/dapp-client-core` or `@nufi/dapp-client-cardano` SDK.

Its advisable to call it as soon as possible as it will also prefetch the Widget, and will make it appear faster when being requested later on.

If no origin is passed to `init` it defaults to `https://wallet.nu.fi`. Note that this default will not work as mainnet is not yet supported.

For now please the origin from the above example. Note that it will you `preprod` network.

#### Initialize SSO login for Cardano

```typescript
import nufiCoreSdk from '@nufi/dapp-client-core'
import {initNufiDappCardanoSdk} from '@nufi/dapp-client-cardano'

// Should be called before accessing `window.cardano.nufiSSO`
initNufiDappCardanoSdk(nufiCoreSdk, 'sso')
const api = await window.cardano.nufiSSO.enable()
```

When called like in the example above users will be asked to choose Web3Auth provider inside the NuFi Widget. If you want to choose specific provider you can pass it using `provider` parameter like this:

```typescript
import nufiCoreSdk from '@nufi/dapp-client-core'
import {initNufiDappCardanoSdk} from '@nufi/dapp-client-cardano'

// Should be called before accessing `window.cardano.nufiSSO`
initNufiDappCardanoSdk(nufiCoreSdk, 'sso', {provider: 'google'})
const api = await window.cardano.nufiSSO.enable()
```

You can currently choose `google` and `discord` providers.

The `initNufiDappCardanoSdk` will populate `window.cardano.nufiSSO` object which has methods corresponding to CIP-30 standard.

#### Listening to social login info changes

You can listen to the changes of current social login info using the following:

```typescript
import nufiCoreSdk from '@nufi/dapp-client-core'

const currentSSOInfo = nufiCoreSdk.getApi().onSocialLoginInfoChanged((data) => {
  // Store data in your app
})
```

Alternatively you can call:

```typescript
import nufiCoreSdk from '@nufi/dapp-client-core'

const currentSSOInfo = nufiCoreSdk.getApi().getSocialLoginInfo()
```

The returned data is either `null` or of the following type

```typescript
export type SocialLoginInfo = {
  email: string | null
  name: string | null
  profileImage: string | null
  typeOfLogin: 'google' | 'discord'
} & Record<string, unknown>
```

#### HideWidget

```typescript
import nufiCoreSdk from '@nufi/dapp-client-core'

nufiCoreSdk.getApi().hideWidget()
```

Use this method to close the Widget in case user logs out using your dapp.

#### Show widget

When calling CIP-30 `enable` method the Widget will be shown automatically.

Therefore if you detect (possibly a flag in your localStorage) that users is logged in you can simply call the `enable` method to make the Widget visible.

#### Use SsoButton for React

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

```jsx
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

```jsx
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

For complete example please check [here](https://github.com/nufi-official/adaplays.xyz/commit/641466c4e8b534f1461692cac6987396b77b5c7c).

#### Selecting Extension provider

For users with NuFi extension installed, there are no specific actions required. Simply access `window.cardano.nufi` from anywhere as it is not controlled by the NuFi Widget SDK.

### Limitations

* Only cardano preprod network is enabled for now.
* The terms and conditions will be updated before going to production.

### Troubleshooting
