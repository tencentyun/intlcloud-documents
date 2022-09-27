The Tencent Effect SDK offers **beautification effects**, **filters**, and **special effects**. They are all supported by the web SDK as well. For filters and special effects, you need to get the resource list first and configure them in the SDK by specifying `EffectId`.

## Beautification
You can pass in beautification parameters during initialization. You can also call `setBeautify` of the SDK to set beautification effects.
- Currently, the SDK supports the following beautification effects:
```typescript
type BeautifyOptions = {
	whiten?: number, // The brightening effect. Value range: 0-1.
	dermabrasion?: number // The smooth skin effect. Value range: 0-1.
	lift?: number // The slim face effect. Value range: 0-1.
	shave?: number // The face width. Value range: 0-1.
	eye?: number // The big eyes effect. Value range: 0-1.
	chin?: number // The chin effect. Value range: 0-1.
}
```
- Call `setBeautify` of the SDK to set beautification effects:
```javascript
sdk.setBeautify({
	whiten: 0.2,
	dermabrasion: 0,
	lift: 0.3,
	shave:0.1,
	eye: 0.9,
	chin: 0
})
```

## Filters
Given the relatively high cost of filter creation, we offer some built-in filters which you can use directly.
1. Get a list of the built-in filters:
```javascript
const filterList = await sdk.getCommonFilter()
```
2. Configure filters
```javascript
sdk.setFilter(filterList[0].EffectId, 0.5)
```


## Special Effects
You can use either the built-in effects of the SDK or the effects you customize in the [console](https://console.cloud.tencent.com/vcube/creator).


```javascript
// Get the built-in effects
// By default, the built-in makeup effects and stickers are returned. You can use the `Label` parameter to specify the type of resources to return.
const presetEffectList = await sdk.getEffectList({
	Type: 'Preset'
	// Label: ['Stickers'] (Return only stickers)
})

// Get the custom effects
const customEffectList = await sdk.getEffectList({
	Type: 'Custom'
})

// Pass in the request parameters of `getEffectList`
const lipList = await sdk.getEffectList({
	PageNumber: 0,
	PageSize: 10,
	Name: '',
	Label: ['Lip makeup'], // Specify the type of resources to return
	Type: 'Custom'
})
const eyeList = await sdk.getEffectList({
	PageNumber: 0,
	PageSize: 10,
	Name: '',
	Label: ['Eye makeup'], // Specify the type of resources to return
	Type: 'Custom'
})
// Configuring special effects
sdk.setEffect([lipList[0].EffectId, eyeList[0].EffectId])

// Specify the effect to use and the strength of the effect
sdk.setEffect([
{
	id: lipList[0].EffectId,
	intensity: 0.5
}, 
{
	id: eyeList[0].EffectId,
	intensity: 0.7
})
// Set only the filter strength
sdk.setEffect([
{
	id: lipList[0].EffectId,
	intensity: 0.5,
	filterIntensity: 0
}, 
{
	id: eyeList[0].EffectId,
	intensity: 0.7,
	filterIntensity: 1
})
```


>! When customizing a special effect, you can add a filter to the effect. In such cases, you can use `filterIntensity` to adjust the strength of the filter.

## Disabling Detection
The performance overhead of AI detection is high. To save your resources, the SDK will automatically disable AI detection when no beautification or special effects are used and enable AI detection again when effects are applied.
```javascript
// Clear all effect settings to disable AI detection
sdk.setBeautify({
	whiten: 0,
	dermabrasion: 0,
	lift: 0,
	shave:0,
	eye: 0,
	chin: 0
})
sdk.setEffect('')
```
