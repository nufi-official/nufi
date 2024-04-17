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
