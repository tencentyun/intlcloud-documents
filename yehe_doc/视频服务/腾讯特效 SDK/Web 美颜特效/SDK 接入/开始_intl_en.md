This document shows you how to quickly and safely integrate the Tencent Effect web SDK and use its features.

## Workflow
The **Tencent Effect web SDK** offers simple and minimally invasive APIs. To integrate it and use its features, you only need to initialize an instance and add the render node to your webpage.
![](https://qcloudimg.tencent-cloud.cn/raw/a691e17a2a028c9fa00a92f37091465b.jpg)

## Installation
The Tencent Effect web SDK is offered as an npm package.
```
npm install tencentcloud-webar
```

## Integration

- We offer two initialization modes for the web SDK.
	- [Built-in camera and player](https://intl.cloud.tencent.com/document/product/1143/50101): The device’s built-in camera and player are used. API calls are easy and fast, with rich interactive features.
	- [Custom streams](https://intl.cloud.tencent.com/document/product/1143/50102): You can use this mode if you want to apply effects to your own streams or want greater flexibility and control.

## Configuration
See [Configuring Filters and Effects](https://intl.cloud.tencent.com/document/product/1143/50104).

## Keying (new feature in v0.2.0)
The keying feature allows you to change the background. It’s only available in the web SDK. For details, see [Configuring Keying](https://intl.cloud.tencent.com/document/product/1143/50105).

## Parameters and APIs
See [Parameters and APIs](https://intl.cloud.tencent.com/document/product/1143/50106).

## Compatibility

| Browser   | Platforms |
| -----   | --- |
| Chrome  | Desktop, Android, iOS |
| Safari  | macOS, iOS |
| Firefox | Desktop, Android, iOS |
| QQ WebView | Android |
| WeChat WebView | Android/iOS (WeChat 8.0.16+)|

>? **The SDK 0.2.1 added support for testing hardware acceleration:**
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

