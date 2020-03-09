This document describes how to quickly integrate the Tencent Cloud IM SDK into your web or WeChat mini program projects.
- You can integrate the IM SDK into your web projects by using NPM (recommended) or scripts.
- You can integrate the IM SDK into your mini program projects by using NPM.

## Preparations
- You have already created an IM application and obtained an SDKAppID.
- You have obtained key information.


## Related Documentation
- [Quick Demo Operation](https://intl.cloud.tencent.com/document/product/1047/34553)
- [Running the IM SDK (Mini Program) Demo](https://github.com/tencentyun/TIMSDK/tree/master/WXMini)
- [Running the IM SDK (Web) Demo](https://github.com/tencentyun/TIMSDK/tree/master/H5)

## Integrating the SDK


### Integrating with NPM (recommended)
Use NPM to install appropriate IM SDK dependencies in your project.

#### **Web project**
```javascript
// IM Web SDK
npm install tim-js-sdk --save
// COS SDK that is required for sending messages such as images and files
npm install cos-js-sdk-v5 --save
```
 >If a problem occurs during dependency synchronization, change the npm source and try again.
>```
>// Changes the cnpm source.
>npm config set registry http://r.cnpmjs.org/
>```
 
 Import modules to the project script.
<pre>
import TIM from 'tim-js-sdk';
import COS from "cos-js-sdk-v5";

let options = {
  SDKAppID: 0 // Replaces 0 with the SDKAppID of your IM application during access.
};
// Creates an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by tim.

// Sets the SDK log level for output. For details on each level, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0); // Indicates the common level. We recommend that you use this level during access as it covers an extensive range of logs.
// tim.setLogLevel(1); // Indicates the release level, at which the SDK outputs important information. We recommend that you use this level in the production environment.

// Registers the COS SDK plugin.
tim.registerPlugin({'cos-js-sdk': COS});
</pre>

#### **Mini program project**
```
// IM mini program SDK
npm install tim-wx-sdk --save
// COS SDK that is required for sending messages such as images and files
npm install cos-wx-sdk-v5 --save
```
>If a problem occurs during dependency synchronization, change the npm source and try again.
>```
>// Changes the cnpm source.
>npm config set registry http://r.cnpmjs.org/
>```

 Import modules to the project script and initialize the script.
<pre>
import TIM from 'tim-wx-sdk';
import COS from "cos-wx-sdk-v5";

let options = {
  SDKAppID: 0 // Replaces 0 with the SDKAppID of your IM application during access.
};
// Creates an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by tim.

// Sets the SDK log level for output. For details on each level, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0); // Indicates the common level. We recommend that you use this level during access as it covers an extensive range of logs.
// tim.setLogLevel(1); // Indicates the release level, at which the SDK outputs important information. We recommend that you use this level in the production environment.

// Registers the COS SDK plugin.
tim.registerPlugin({'cos-wx-sdk': COS});
</pre>

For more information on the initialization process and the use of APIs, see [SDK Initialization](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html).

### Script integration
Import the SDK to your project by using the script tag and initialize the SDK.

```html
<!-- tim-js.js can be obtained at https://github.com/tencentyun/TIMSDK/tree/master/H5/sdk -->
<script src="./tim-js.js"></script>
<!-- cos-js-sdk-v5.min.js can be obtained at https://github.com/tencentyun/cos-js-sdk-v5/tree/master/dist -->
<script src="./cos-js-sdk-v5.min.js"></script>
<script>
var options = {
  SDKAppID: 0 // Replaces 0 with the SDKAppID of your IM application during access.
};
// Creates an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
var tim = TIM.create(options);
// Sets the SDK log level for output. For details on each level, see setLogLevel API description.
tim.setLogLevel(0); // Indicates the common level. We recommend that you use this level during access as it covers an extensive range of logs.
// tim.setLogLevel(1); // Indicates the release level, at which the SDK outputs important information. We recommend that you use this level in the production environment.

// Registers the COS SDK plugin.
tim.registerPlugin({'cos-js-sdk': COS});

// You can then bind events and build IM apps through tim.
</script>
```

>Sets the SDK log level for output. For details on each level, see [setLogLevel API Description](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel).

For more information on the initialization process and the use of APIs, see [SDK Initialization](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html).

### Related resources
- [SDK Changelog](https://cloud.tencent.com/document/product/269/38492)
- [SDK API Documentation](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html)
- [FAQs](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/tutorial-01-faq.html)
- [IM Web Demo](https://github.com/tencentyun/TIMSDK/tree/master/H5)
- [Download URL of the Tencent Cloud COS JS SDK](https://github.com/tencentyun/cos-js-sdk-v5)


## FAQs

**1. What should I do if I want to launch a mini program or deploy an official environment?**
Configure domain names by navigating to **WeChat Official Accounts Platform** > **Development** > **Development Settings** > **Server Domain Name**:

Add the following domain names to **request valid domain names**:

| Domain Name | Description | Required |
|:-------:|---------|----|
| `https://webim.tim.qq.com` | Web IM service domain | Yes |
| `https://yun.tim.qq.com` | Web IM service domain | Yes |
| `https://events.tim.qq.com` | Web IM service domain | Yes |
| `https://grouptalk.c2c.qq.com`| Web IM service domain | Yes |
| `https://pingtas.qq.com` | Web IM statistical domain name | Yes |

Add the following domain name to the **uploadFile valid domain name**:

| Domain Name | Description | Required |
|:-------:|---------|----|
| `https://cos.ap-shanghai.myqcloud.com` | Domain name for uploading files | Yes |

Add the following domain names to **downloadFile valid domain names**:

| Domain Name | Description | Required |
|:-------:|---------|----|
| `https://cos.ap-shanghai.myqcloud.com` | Domain name for downloading files | Yes |
