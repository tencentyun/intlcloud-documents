This document describes how to quickly integrate the Tencent Cloud IM SDK into your web, Mini Program, or uni-app project.

## Integrating the SDK

- You can integrate the IM SDK into your web project by using npm (recommended) or script.
- You can integrate the IM SDK into your Mini Program or uni-app project by using npm.
- You can integrate the SDK upload plugin for faster and safer upload of rich text message resources. For more information, see [tim-upload-plugin](https://www.npmjs.com/package/tim-upload-plugin).

### Integration via npm (recommended)

Use npm to install appropriate IM SDK dependencies in your project.

#### **Web project**

<dx-codeblock>
:::  js
// IM Web SDK
// SDK v2.11.2 and later versions support WebSocket, and you are advised to integrate such SDK versions. SDK v2.10.2 and earlier versions use HTTP.
npm install tim-js-sdk --save
// The Tencent Cloud IM upload plugin is required to send messages such as images and files.
npm install tim-upload-plugin --save
:::
</dx-codeblock>

>?If a problem occurs during dependency synchronization, change the npm source and try again.
><dx-codeblock>
:::  js

npm config set registry http://r.cnpmjs.org/

:::
</dx-codeblock>


 Import the module into the project script.
<dx-codeblock>
:::  js

// SDK v2.11.2 and later versions support WebSocket, and you are advised to integrate such SDK versions. SDK v2.10.2 and earlier versions use HTTP.
import TIM from 'tim-js-sdk';
import TIMUploadPlugin from 'tim-upload-plugin';

let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM application when connecting
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by tim.

// Set the SDK logging level. For more information on each level, see the setLogLevel API description at https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setLogLevel.</a>
tim.setLogLevel(0); // Common level. You are advised to use this level during access as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.

// Register the Tencent Cloud IM upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});

:::
</dx-codeblock>

#### **Mini program or uni-app project**

<dx-codeblock>
:::  js

// SDK v2.11.2 and later versions support WebSocket, and you are advised to integrate such SDK versions. SDK v2.10.2 and earlier versions use HTTP.
npm install tim-wx-sdk --save
// The Tencent Cloud IM upload plugin is required to send messages such as images and files.
npm install tim-upload-plugin --save

:::
</dx-codeblock>

>?If a problem occurs during dependency synchronization, change the npm source and try again.
><dx-codeblock>
:::  js

npm config set registry http://r.cnpmjs.org/

:::
</dx-codeblock>

Import modules to the project script and initialize the modules.
<dx-codeblock>
:::  js
// SDK v2.11.2 and later versions support WebSocket, and you are advised to integrate such SDK versions. SDK v2.10.2 and earlier versions use HTTP.
import TIM from 'tim-wx-sdk';
import TIMUploadPlugin from 'tim-upload-plugin';

let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM application when connecting
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by tim.

// Set the SDK logging level. For more information on each level, see the setLogLevel API description at https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setLogLevel.</a>
tim.setLogLevel(0); // Common level. You are advised to use this level during access as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.

// Register the Tencent Cloud IM upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});

// In v2.22.0 or later, the offline push plugin can be used if native apps are packaged using uni-app.
// Attention: To meet compliance requirements, after the user agrees to the privacy policy and logs in successfully, the SDK obtains the push token through the push plugin and delivers the push token to the background. (If the token fails to be obtained, the offline push feature cannot work properly.)
const TUIOfflinePush = uni.requireNativePlugin("TencentCloud-TUIOfflinePush");
tim.registerPlugin({
  'tim-offline-push-plugin': TUIOfflinePush,
  'offlinePushConfig': {
    // Huawei
    'huaweiBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the IM console
    // Mi
    'xiaomiBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the IM console
    'xiaomiAppID': '', // `APPID` assigned by the Mi Developer platform
    'xiaomiAppKey': '', // `APPKEY` assigned by the Mi Developer platform
    // Meizu
    'meizuBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the IM console
    'meizuAppID': '', // `APPID` assigned by the Meizu Flyme platform
    'meizuAppKey': '', // `APPKEY` assigned by the Meizu Flyme platform
    // vivo
    'vivoBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the IM console
    // OPPO
    'oppoBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the IM console
    'oppoAppKey': '', // `APPID` assigned by the OPPO Developers platform
    'oppoAppSecret': '', // `Secret` assigned by the OPPO Developers platform
    // iOS
    'iosBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the IM console
  }
});

:::
</dx-codeblock>

### Integrating via script

Import the SDK to your project by using the script tag and initialize the SDK.

<dx-codeblock>
:::  js

<!-- `tim-js.js` and `tim-upload-plugin.js` can be obtained at https://github.com/TencentCloud/TIMSDK/tree/master/Web/IMSDK. -->
<script src="./tim-js.js"></script>
<script src="./tim-upload-plugin.js"></script>
<script>
var options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM application when connecting
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
var tim = TIM.create(options);
// Set the SDK log output level. For details on each level, see **setLogLevel API description**.
tim.setLogLevel(0); // Common level. You are advised to use this level during access as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.

// Register the Tencent Cloud IM upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});

// Next, you can use `tim` to bind events and build IM apps.
</script>

:::
</dx-codeblock>


### Relevant resources
- [SDK Update Log](https://intl.cloud.tencent.com/document/product/1047/34281)
- [SDK API Documentation](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [IM Web Demo](https://github.com/TencentCloud/TIMSDK/tree/master/Web)
- [Download URL of Tencent Cloud IM Upload Plugin](https://www.npmjs.com/package/tim-upload-plugin)
