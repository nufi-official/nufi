# Widget options

Following is a set of options that allows
to customize widget appearance and positioning.

To specify the options, use the second parameter
of the `nufiCoreSdk.init` function when initializing the widget.

## Z-index

If you have some elements on your page with higher
z-index that can potentially overlap with our widget, you can set the z-index of the widget to a higher value using the code below:

```typescript
nufiCoreSdk.init(nufiDomain, {
  // supply any value you wish, the default is 0
  zIndex: 99999,
})
```

## Overriding widget position

If the default position of the widget (bottom left of your webpage) doesn't suit you, you can simply override it with CSS, using widget's iframe id attribute, e.g.:

```css
iframe#nufi-widget {
  bottom: 100px !important
  left: inherit !important
  right: 16px
  // whatever else
}
```

## Featuring custom tokens

You can "feature" tokens that you dapp manages to be displayed at the top of the
user tokens list section. Note that you can feature only up to two tokens. If you try to feature more, the rest of the tokens would be ignored.
Also note that if user has no funds in the wallet no tokens are listed.
The list of featured tokens can be passed in the `initNufiDappCardanoSdk()` call:

```typescript
initNufiDappCardanoSdk(nufiCoreSdk, platform, {
    featuredTokens: [{
      assetNameHex: 'YOUR_ASSET_NAME_HEX',
      policyIdHex: 'YOUR_POLICY_ID_HEX'
    }]
  })
```

## Color mode

You can choose from `dark` and `light` color mode. Note that default value is `dark`.
The color mode you choose will only take effect if users did not change it on their
own, otherwise user's choice takes precedence.

```typescript
nufiCoreSdk.init(nufiDomain, {
  colorMode: 'dark' | 'light'
})
```

## Manual Widget collapse/expand & visibility status

You can use the following methods to get widget visibility status on demand,
and open/close it on your own. This can be handy if your dapp manages more complex
UX flow, otherwise we suggest you to avoid using these methods.

Note that as of now it is not possible to subscribe to the widget visibility status changes.

```typescript
nufiCoreSdk.getApi().getWidgetVisibilityStatus() // 'closed' | 'hidden' | 'open'
nufiCoreSdk.getApi().showWidget('opened')
nufiCoreSdk.getApi().showWidget('closed')
```

## Responsive mode

Use this option to activate responsive behavior for mobile devices.
If we used we will detect whether to serve responsive or standard
version of the widget.

```typescript
nufiCoreSdk.init(nufiDomain, {
  responsive: true
})
```
