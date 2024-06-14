# Using multiple providers

This section is relevant to you, if your dapp wants to support
more than one NuFi SDK provider (Snap / NuFiConnect) or wants
to use NuFiConnect with more blockchains. Note that currently only
Cardano is being supported.

*The takeaway is that before accessing some provider, the last invocation of `initNufiDappCardanoSdk` has to be called with the settings matching this provider.*

### Example: Changing NuFi SDK providers
To showcase the usage please consider the below example:

* User clicks on "Metamask" icon in your dapp
* The dapp calls `initNufiDappCardanoSdk(nufiCoreSdk, 'snap')`
* Dapp can now access `window.cardano.nufiSnap`
* User is finished using the snap, disconnects and clicks on "NuFiConnect" social button
* The dapp calls `initNufiDappCardanoSdk(nufiCoreSdk, 'sso')`
* Dapp can now access `window.cardano.nufiSSO`
* Accessing `window.cardano.nufiSnap` will no longer work correctly!
* If you need to access `window.cardano.nufiSnap` again, you need to call `initNufiDappCardanoSdk(nufiCoreSdk, 'snap')` before that
