# Migrations

## Migrating to v0.6.0

The `getApi` call was deprecated as its synchronous nature lead to calls being ignored
if the widget did not have enough time to load.

The properties previously accessed by `getApi` call are available using following calls:

```typescript
import nufiCoreSdk from '@nufi/dapp-client-core'

nufiCoreSdk.isMetamaskInstalled
nufiCoreSdk.onSocialLoginInfoChanged
nufiCoreSdk.getSocialLoginInfo
```

Or are available via `getWidgetApi` call that returns promise:

```typescript
import nufiCoreSdk from '@nufi/dapp-client-core'

const widgetApi = await nufiCoreSdk.getWidgetApi()

widgetApi.showWidget
widgetApi.hideWidget
widgetApi.getWidgetVisibilityStatus
widgetApi.signOut
```
