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
