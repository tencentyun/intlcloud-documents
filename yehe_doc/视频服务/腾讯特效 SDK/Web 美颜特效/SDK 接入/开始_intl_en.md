The [Tencent Effect web SDK](https://www.tencentcloud.com/document/product/1143/51226) allows you to quickly and securely integrate Tencent Effect capabilities into your project.

## Workflow
The **Tencent Effect web SDK** offers simple and minimally invasive APIs. To use its features, you only need to initialize an instance and add a render node to your webpage.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a691e17a2a028c9fa00a92f37091465b.jpg" style="zoom:50%;" />

## Installation
The Tencent Effect web SDK is offered as an npm package.
```
npm install tencentcloud-webar
```

## Integrating the SDK

- We offer two initialization modes for the web SDK.
	- [Built-in camera and player](https://intl.cloud.tencent.com/document/product/1143/50101): The device’s built-in camera and player are used. API calls are easy and fast, with rich interactive features.
	- [Custom streams](https://intl.cloud.tencent.com/document/product/1143/50102): You can use this mode if you want to apply effects to your own streams or want greater flexibility and control.

## Configuring Filters and Effects
See [Configuring Filters and Effects](https://intl.cloud.tencent.com/document/product/1143/50104).

## Keying (New in v0.2.0)
The keying feature allows you to change the background. For details, see [Configuring Keying](https://intl.cloud.tencent.com/document/product/1143/50105).

## 3D Effects (New in v0.3.0)
You can configure 3D effects the same way you configure other effects. For details, see [Configuring Filters and Effects](https://www.tencentcloud.com/document/product/1143/50104).

## Animojis and Virtual Avatars (New in v0.3.0)
This capability relies on a WebGL2 environment. For details, see [Using Animojis and Virtual Avatars](https://www.tencentcloud.com/document/product/1143/51231).


## Parameters and APIs
See [Parameters and APIs](https://intl.cloud.tencent.com/document/product/1143/50106).

## Compatibility

| Browser   | Platforms |
| -----   | --- |
| Chrome  | Desktop, Android, iOS |
| Safari  | Desktop, iOS |
| Firefox | Desktop, Android, iOS |
| QQ WebView | Android |
| WeChat WebView | Android/iOS (WeChat 8.0.16+)|


>? **The SDK 0.2.1 added support for checking hardware acceleration:**
The Tencent Effect web SDK relies on hardware acceleration to achieve smooth rendering. The SDK allows you to check whether a browser supports hardware acceleration. You can block the browser if it does not support hardware acceleration.
```javascript
import {ArSdk, isWebGLSupported} from 'tencentcloud-webar'

if(isWebGLSupported()) {
	const sdk = new ArSdk({
		...
	})
} else {
	// The browser blocking logic
}
```
