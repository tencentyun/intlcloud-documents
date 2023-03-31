This document describes how to quickly integrate the Tencent Cloud Chat SDK into your web, mini program, or uni-app project.

## Integrating the SDK

- You can integrate the Chat SDK into your web project by using npm (recommended) or script.
- You can integrate the Chat SDK into your mini program or uni-app project by using npm.
- You can integrate the upload plugin for faster and safer upload of rich text message resources. For more information, see [tim-upload-plugin](https://www.npmjs.com/package/tim-upload-plugin).
- You can integrate the local moderation plug-in [tim-profanity-filter-plugin](https://www.npmjs.com/package/tim-profanity-filter-plugin) to moderate the text content sent by the Chat SDK on the client locally. The plug-in can intercept or replace configured sensitive words in the text content to ensure your product experience and business security.

### Integration via npm (recommended)

Use npm to install appropriate Chat SDK dependencies in your project.

#### **Web project**

<dx-codeblock>
:::  js
// Web SDK
// SDK v2.11.2 and later versions support WebSocket, and you are advised to integrate such SDK versions. SDK v2.10.2 and earlier versions use HTTP.
npm install tim-js-sdk --save
// The Tencent Cloud Chat upload plugin is required to send messages such as images and files.
npm install tim-upload-plugin --save
// The local moderation plug-in is needed to intercept or replace sensitive words.
npm install tim-profanity-filter-plugin --save
:::
</dx-codeblock>

>?If a problem occurs during dependency synchronization, change the npm source and try again.
><dx-codeblock>
>:::  js

npm config set registry http://r.cnpmjs.org/

:::
</dx-codeblock>


 Import the module into the project script.
<dx-codeblock>
:::  js

// SDK v2.11.2 and later versions support WebSocket, and you are advised to integrate such SDK versions. SDK v2.10.2 and earlier versions use HTTP.
// Starting from v2.24.0, the SDK supports the local moderation plug-in.
import TIM from 'tim-js-sdk';
import TIMUploadPlugin from 'tim-upload-plugin';
import TIMProfanityFilterPlugin from 'tim-profanity-filter-plugin';

let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your Chat application when connecting
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by tim.

// Set the SDK logging level. For more information on each level, see the setLogLevel API description at https://web.sdk.qcloud.com/im/doc/en/SDK.html#setLogLevel.</a>
tim.setLogLevel(0); // Common level. You are advised to use this level during access as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.

// Register the Tencent Cloud Chat upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});

// Register the Tencent Cloud Chat local moderation plug-in.
tim.registerPlugin({'tim-profanity-filter-plugin': TIMProfanityFilterPlugin});

:::
</dx-codeblock>

#### **Mini program or uni-app project**

<dx-codeblock>
:::  js

// SDK v2.11.2 and later versions support WebSocket, and you are advised to integrate such SDK versions. SDK v2.10.2 and earlier versions use HTTP.
npm install tim-wx-sdk --save
// The Tencent Cloud Chat upload plugin is required to send messages such as images and files.
npm install tim-upload-plugin --save
// The local moderation plug-in is needed to intercept or replace sensitive words.
npm install tim-profanity-filter-plugin --save
:::
</dx-codeblock>

>?If a problem occurs during dependency synchronization, change the npm source and try again.
><dx-codeblock>
>:::  js

npm config set registry http://r.cnpmjs.org/

:::
</dx-codeblock>

Import modules to the project script and initialize the modules.
<dx-codeblock>
:::  js
// SDK v2.11.2 and later versions support WebSocket, and you are advised to integrate such SDK versions. SDK v2.10.2 and earlier versions use HTTP.
// Starting from v2.24.0, the SDK supports the local moderation plug-in.
import TIM from 'tim-wx-sdk';
import TIMUploadPlugin from 'tim-upload-plugin';
import TIMProfanityFilterPlugin from 'tim-profanity-filter-plugin';

let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your Chat application when connecting
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by tim.

// Set the SDK logging level. For more information on each level, see the setLogLevel API description at https://web.sdk.qcloud.com/im/doc/en/SDK.html#setLogLevel.</a>
tim.setLogLevel(0); // Common level. You are advised to use this level during access as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.

// Register the Tencent Cloud Chat upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});

// Register the Tencent Cloud Chat local moderation plug-in.
tim.registerPlugin({'tim-profanity-filter-plugin': TIMProfanityFilterPlugin});

// In v2.22.0 or later, the offline push plugin can be used if native apps are packaged using uni-app.
// Attention: To meet compliance requirements, after the user agrees to the privacy policy and logs in successfully, the SDK obtains the push token through the push plugin and delivers the push token to the background. (If the token fails to be obtained, the offline push feature cannot work properly.)
const TUIOfflinePush = uni.requireNativePlugin("TencentCloud-TUIOfflinePush");
tim.registerPlugin({
  'tim-offline-push-plugin': TUIOfflinePush,
  'offlinePushConfig': {
    // Huawei
    'huaweiBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the Chat console
    // Mi
    'xiaomiBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the Chat console
    'xiaomiAppID': '', // `APPID` assigned by the Mi Developer platform
    'xiaomiAppKey': '', // `APPKEY` assigned by the Mi Developer platform
    // Meizu
    'meizuBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the Chat console
    'meizuAppID': '', // `APPID` assigned by the Meizu Flyme platform
    'meizuAppKey': '', // `APPKEY` assigned by the Meizu Flyme platform
    // vivo
    'vivoBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the Chat console
    // OPPO
    'oppoBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the Chat console
    'oppoAppKey': '', // `APPID` assigned by the OPPO Developers platform
    'oppoAppSecret': '', // `Secret` assigned by the OPPO Developers platform
    // iOS
    'iosBusinessID': '', // Certificate ID assigned after a third-party push certificate is uploaded in the Chat console
  }
});

:::
</dx-codeblock>

### Integrating via script

Import the SDK to your project by using the script tag and initialize the SDK.

<dx-codeblock>
:::  js

<script src="./tim-js.js"></script>
<script src="./tim-upload-plugin.js"></script>
<script>
var options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your Chat application when connecting
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
var tim = TIM.create(options);
// Set the SDK log output level. For details on each level, see **setLogLevel API description**.
tim.setLogLevel(0); // Common level. You are advised to use this level during access as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.

// Register the Tencent Cloud Chat upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});

// Next, you can use `tim` to bind events and build Chat apps.
</script>

:::
</dx-codeblock>


### Relevant resources
- [SDK Update Log](https://intl.cloud.tencent.com/document/product/1047/34281)
- [SDK API Documentation](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [WebSocket Upgrade Guide](https://web.sdk.qcloud.com/im/doc/en/tutorial-02-upgradeguideline.html)

## FAQs

**1. Are there any open-source UI components that can be reused or redeveloped?**
Tencent Cloud Chat provides open-source UIKits for all platforms that can be reused or redeveloped by developers. Find the reference documentation below:
- [Get Started (Web)](https://www.tencentcloud.com/document/product/1047/45912)

**2. What should I do if I want to launch a Mini Program and deploy a production environment?**
Configure domain names by navigating to **Weixin Official Accounts Platform** > **Development** > **Development Settings** > **Server Domain Name**:

SDK v2.11.2 and later versions support WebSocket, and the following domain names must be added as **valid socket domain names** for WebSocket:

|        Domain Name        | Description             | Required |
| :-----------------------: | ----------------------- | -------- |
| `wss://wss.im.qcloud.com` | Web Chat service domain | Yes      |
|  `wss://wss.tim.qq.com`   | Web Chat service domain | Yes      |

Add the following domain names to **request valid domain names**:

|          Domain Name           | Description             | Required |
| :----------------------------: | ----------------------- | -------- |
|  `https://web.sdk.qcloud.com`  | Web Chat service domain | Yes      |
|   `https://webim.tim.qq.com`   | Web Chat service domain | Yes      |
|  `https://api.im.qcloud.com`   | Web Chat service domain | Yes      |
| `https://events.im.qcloud.com` | Web Chat service domain | Yes      |

SDK v2.10.2 or earlier versions use HTTP, and the following domain names must be added as the **valid request domain names** for HTTP:

|          Domain Name           | Description                 | Required |
| :----------------------------: | --------------------------- | -------- |
|   `https://webim.tim.qq.com`   | Web Chat service domain     | Yes      |
|    `https://yun.tim.qq.com`    | Web Chat service domain     | Yes      |
|  `https://events.tim.qq.com`   | Web Chat service domain     | Yes      |
| `https://grouptalk.c2c.qq.com` | Web Chat service domain     | Yes      |
|    `https://pingtas.qq.com`    | Web Chat statistical domain | Yes      |

Add the following domain name to the **uploadFile valid domain name**:

|               Domain Name               | Description        | Required |
| :-------------------------------------: | ------------------ | -------- |
| `https://cos.ap-shanghai.myqcloud.com`  | File upload domain | Yes      |
| `https://cos.ap-shanghai.tencentcos.cn` | File upload domain | Yes      |
| `https://cos.ap-guangzhou.myqcloud.com` | File upload domain | Yes      |

Add the following domain name to **downloadFile valid domain name**:

|               Domain Name               | Description          | Required |
| :-------------------------------------: | -------------------- | -------- |
| `https://cos.ap-shanghai.myqcloud.com`  | File download domain | Yes      |
| `https://cos.ap-shanghai.tencentcos.cn` | File download domain | Yes      |
| `https://cos.ap-guangzhou.myqcloud.com` | File download domain | Yes      |

|      |      |      |
|:-------:|---------|----|
|      |      |      |
|      |      |      |
|      |      |      |
