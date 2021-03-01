This document describes how to quickly integrate the Tencent Cloud IM SDK into your web or Mini Program project.
- You can integrate the IM SDK into your web project by using NPM (recommended) or scripts.
- You can integrate the IM SDK into your Mini Program project by using NPM.


## Preparations
- You have already created an IM app and obtained the `SDKAppID`.
- You have obtained the key information.


## Documentation
- [Demo Quick Start](https://intl.cloud.tencent.com/document/product/1047/34553)
- [Running the IM SDK (Mini Program) Demo](https://github.com/tencentyun/TIMSDK/tree/master/WXMini)
- [Running the IM SDK (Web) Demo](https://github.com/tencentyun/TIMSDK/tree/master/H5)

## Integrating the SDK


### Integrating with NPM (recommended)
Use NPM to install appropriate IM SDK dependencies in your project.

#### **Web project**
```javascript
// IM Web SDK
npm install tim-js-sdk --save
// The Tencent Cloud IM upload plugin is required to send messages such as image and files.
npm install tim-upload-plugin --save
```
 >?If a problem occurs during dependency synchronization, change the npm source and try again.
>```
>// Change cnpm source
>npm config set registry http://r.cnpmjs.org/
>```

 Import the module into the project script:
```
import TIM from 'tim-js-sdk';
import TIMUploadPlugin from 'tim-upload-plugin';

let options = {
  SDKAppID: 0 // Replace `0` with the `SDKAppID` of your IM app during connection.
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by `tim`.

// Set the SDK log output level. For more information on each level, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0); // Common level. You are advised to use this level during connection as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.

// Register the Tencent Cloud IM upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});
```

#### **Mini Program project**
```javascript
// IM Mini Program SDK
npm install tim-wx-sdk --save
// The Tencent Cloud IM upload plugin is required to send messages such as image and files.
npm install tim-upload-plugin --save
```
>?If a problem occurs during dependency synchronization, change the npm source and try again.
>```
>// Change cnpm source
>npm config set registry http://r.cnpmjs.org/
>```

 Import modules to the project script and initialize the SDK.
```
import TIM from 'tim-wx-sdk';
import TIMUploadPlugin from 'tim-upload-plugin';

let options = {
  SDKAppID: 0 // Replace `0` with the `SDKAppID` of your IM app during connection.
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by `tim`.

// Set the SDK log output level. For more information on each level, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0); // Common level. You are advised to use this level during connection as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.

// Register the Tencent Cloud IM upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});
```

For more information on how to initialize the SDK and use APIs, see [SDK Initialization](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html).

### Integrating via script
Import the SDK to your project by using the script tag and initialize the SDK.

```html
<!-- `tim-js.js` and `tim-upload-plugin.js` can be obtained at https://github.com/tencentyun/TIMSDK/tree/master/H5/sdk. -->
<script src="./tim-js.js"></script>
<script src="./tim-upload-plugin.js"></script>
<script>
var options = {
  SDKAppID: 0 // Replace `0` with the `SDKAppID` of your IM app during connection.
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
var tim = TIM.create(options);
// Set the SDK log output level. For details on each level, see **setLogLevel API description**.
tim.setLogLevel(0); // Common level. You are advised to use this level during connection as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.

// Register the Tencent Cloud IM upload plugin.
tim.registerPlugin({'tim-upload-plugin': TIMUploadPlugin});

// Next, you can use `tim` to bind events and build IM apps.
</script>
```

>?Set the SDK log output level. For more information on each level, see [setLogLevel API Description](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel).

For more information on how to initialize the SDK and use APIs, see [SDK Initialization](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html).

### Relevant resources
- [SDK Update Log](https://intl.cloud.tencent.com/document/product/1047/34281)
- [SDK API Documentation](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html)
- [FAQs](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/tutorial-01-faq.html)
- [IM Web Demo](https://github.com/tencentyun/TIMSDK/tree/master/H5)
- [Download URL of Tencent Cloud IM Upload Plugin](https://www.npmjs.com/package/tim-upload-plugin)


## FAQs

**1. What should I do if I want to launch a Mini Program and deploy a production environment?**
Configure domain names by navigating to **WeChat Official Accounts Platform** > **Development** > **Development Settings** > **Server Domain Name**:

Add the following domain names to **request valid domain names**:

| Domain | Description |  Required |
|:-------:|---------|----|
|`https://webim.tim.qq.com` | Web IM service domain | Yes |
|`https://yun.tim.qq.com` | Web IM service domain | Yes |
|`https://events.tim.qq.com` | Web IM service domain | Yes |
|`https://grouptalk.c2c.qq.com`| Web IM service domain | Yes |
|`https://pingtas.qq.com` | Web IM statistical domain | Yes |

Add the following domain name to the **uploadFile valid domain name**:

| Domain | Description |  Required |
|:-------:|---------|----|
|`https://cos.ap-shanghai.myqcloud.com` | File upload domain | Yes |

Add the following domain name to **downloadFile valid domain name**:

| Domain | Description |  Required |
|:-------:|---------|----|
|`https://cos.ap-shanghai.myqcloud.com` | File download domain | Yes |

