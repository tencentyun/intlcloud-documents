## Overview
[tim-upload-plugin](https://www.npmjs.com/package/tim-upload-plugin) is an upload plugin of Tencent Cloud IM. It upload resources in a way based on the Tencent Cloud COS pre-signed URL method. When integrating Tencent Cloud IM, you can use [tim-upload-plugin](https://www.npmjs.com/package/tim-upload-plugin) instead of "cos-js-sdk" or "cos-wx-sdk" to upload resource. This plugin not only helps improve the security of application data, but also has benefits such as fast upload speed, small size, and support for Mini Programs on multiple platforms.

## Advantages

- ### Improved security of application data
You receive a new pre-signed URL every time you upload a resource file. The pre-signed URL is bound with the current file type and file information. In addition, pre-signed URLs have an expiration time and cannot be used after they expire.

- ### 10% to 50% increase in average upload speed
	- The average speed of uploading a resource file within 5 MB is 50% faster than that of "cos-js-sdk" and "cos-wx-sdk".
	- The average speed of uploading a resource file between 5 MB and 12 MB is 30% faster than that of "cos-js-sdk" and "cos-wx-sdk".

- ### Support for Mini Programs on multiple platforms
"tim-upload-plugin" provides better compatibility with Mini Programs on different platforms. Currently, it can be used when you are integrating Tencent Cloud IM into WeChat, QQ, Baidu, Toutiao, and Alipay Mini Programs, while "cos-wx-sdk" only supports integration into WeChat Mini Programs.

- ### Support for various file formats
Currently, it supports JPG, JPEG, PNG, BMP, and GIF images, MP4 videos, audio files, as well as Word, Excel, and PDF files.

- ### Lightweight
Its size is less than 10 KB. Compared with "cos-js-sdk" (1.8 MB) and "cos-wx-sdk" (1.2 MB), "tim-upload-plugin" is 98% smaller in size, which helps reduce your application size.

## How It Works
![](https://main.qcloudimg.com/raw/dfd72072899f834e5fc26d942e3be13c.png)

## Notes:

- Before using "tim-upload-plugin", please upgrade "tim-js-sdk" or "tim-wx-sdk" to v2.9.2 or above.
- To use "tim-upload-plugin" on a Mini Program terminal, you need to configure the valid domain (https://cos.ap-shanghai.myqcloud.com) of `uploadFile` and `downloadFile` in the Mini Program console.
- Do not register "tim-upload-plugin" and "cos-js-sdk" or "cos-wx-sdk" at the same time. IM SDK will check "tim-upload-plugin" first.
- Currently, "tim-upload-plugin" cannot be used in the Node.js environment.

## Access
Before accessing tim-upload-plugin, you need to upgrade your Tencent Cloud IM SDK to v2.9.2 or above.

### 1. Access via npm

```javascript
// Download the dependency.
npm i tim-upload-plugin --save
// To integrate "tim-upload-plugin", your "tim-js-sdk" or "tim-wx-sdk" version should be v2.9.2 or above.
npm i tim-js-sdk@latest --save // Used in web environment.
// npm i tim-wx-sdk@latest --save // Used in Mini Program environment.

// Import the modules to the project script and initialize it.
import TIM from 'tim-js-sdk' // Used in web environment.
// import TIM from 'tim-wx-sdk'; // Used in Mini Program environment.
import TIMUploadPlugin from 'tim-upload-plugin';

let options = {
  SDKAppID: 0 // Replace `0` with the `SDKAppID` of your IM app during access.
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by `tim`.

// Set the SDK log output level. For details on each level, see **setLogLevel API description**.
tim.setLogLevel(0); // Common level. You are advised to use this level during access as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.

// Register the Tencent Cloud IM upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});
```

### 2. Access via script

```html
<!-- `tim-js.js` and `tim-upload-plugin.js` can be obtained at https://github.com/tencentyun/TIMSDK/tree/master/Web/Demo/sdk. -->
<script src='./tim-js.js'></script>
<script src='./tim-upload-plugin.js'></script>
<script>
let options = {
  SDKAppID: 0 // Replace `0` with the `SDKAppID` of your IM app during access.
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options);
// Set the SDK log output level. For details on each level, see **setLogLevel API description**.
tim.setLogLevel(0); // Common level. You are advised to use this level during access as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.

// Register the Tencent Cloud IM upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});

// Next, you can use `tim` to bind events and build IM apps.
</script>
```


