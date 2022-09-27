To use the keying feature, you need to enable the keying module when initializing the SDK. For details, see [Custom Stream or Image](https://intl.cloud.tencent.com/document/product/1143/50102) and [Built-in Camera](https://intl.cloud.tencent.com/document/product/1143/50101).
**This feature is only available in the web SDK**.

[](id:set)
## Setting the Background
- The SDK allows you to blur the background or set an image as the background. You can pass in keying parameters during initialization.
```javascript
const config = {
	module: {
		beautify: true, // Whether to enable the effect module, which offers beautification and makeup effects as well as stickers
		segmentation: true // Whether to enable the keying module, which allows you to change the background
	},
	auth: authData, // The authentication information
	input: stream, // The input stream
	beautify: { // The effect parameters for initialization (optional)
		whiten: 0.1,
		dermabrasion: 0.3,
		eye: 0.2,
		chin: 0,
		lift: 0.1,
		shave: 0.2
	},
	background: {
		type: 'blur' // Blur the background
	}
}
const sdk = new ArSdk(
	// Pass in a config object to initialize the SDK
	config
)
```
- You can also dynamically change the background.
```javascript
sdk.setBackground({
	type: 'image', // The background image
	src: 'https://webar-static.tencent-cloud.com/assets/background/1.jpg'
})
```

[](id:open)
## Using Transparent Backgrounds
The SDK supports transparent backgrounds on some browsers.
```javascript
sdk.setBackground({
	type: 'transparent'
})
```

>! Please pay attention to the following:
>- Keying is supported on both mobile and desktop browsers.
>- Because WebRTC does not support alpha channels, you can only use transparent backgrounds locally. Background transparency will not work after publishing.
>- Background transparency is supported on desktop Chrome and Firefox, but not supported on desktop or mobile Safari.
