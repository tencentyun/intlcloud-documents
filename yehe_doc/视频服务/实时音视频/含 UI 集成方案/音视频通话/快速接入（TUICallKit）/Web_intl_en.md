# Integrating TUICallKit

This document shows you how to quickly integrate the `TUICallKit` component to build a video call application with ready-made UI.

To try out the component, see [TUICallKit basic demo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md).

Before you start, check whether your desktop browser supports TRTC. For details, see [Environment requirements](#3-Environment requirements).

## Contents
* [Step 1. Activate TRTC and IM](#Step 1. Activate TRTC and IM)
* [Step 2: Integrate TUICallKit](Step 2: Integrate TUICallKit)
* [Step 3. Call `TUICallKit`](#Step 3. Call `TUICallKit`)
* [Related documents](#Related documents)
* [FAQs](#FAQs)
  + [1. How do I generate a UserSig?](#1-How do I generate a UserSig?)
  + [2. Vite import](#2-Vite import)
  + [3. Environment requirements](#3-Environment requirements)
    - [Browser versions](#Browser versions)
    - [Network](#Network)
    - [Website domain protocol](#Website domain protocol)

## Step 1. Activate TRTC and IM

`TUICallKit` is based on two paid PaaS products of Tencent Cloud: [Instant Messaging (IM)](https://intl.cloud.tencent.com/document/product/1047/35448) and [TRTC](https://intl.cloud.tencent.com/document/product/647/35078). Follow the steps below to activate the two services and a 60-day free trial:

1. Log in to the [IM console](https://console.cloud.tencent.com/im), and click **Create Application**. In the pop-up window, enter your application name and click **Confirm**.

<!-- <img style="width:600px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/1105c3c339be4f71d72800fe2839b113.png"/>  -->

![](https://qcloudimg.tencent-cloud.cn/raw/ce2e34f7cd1cd14679fc5decffb469af.png)

2. Click the application you created. On the **Basic Configuration** page, find **Tencent Real-Time Communication** in the bottom right and click **Try now** to activate the 60-day free trial.

<div align="center">
<!-- <img style="width:600px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/667633f7addfd0c589bb086b1fc17d30.png"/>  -->

![](https://qcloudimg.tencent-cloud.cn/raw/796e49d9f55174aacb62bb8eb848feaf.png)

3. On the same page, find and record the **SDKAppID** and **Key**, which will be used in subsequent steps.

<!-- <img style="width:600px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/e435332cda8d9ec7fea21bd95f7a0cba.png"/>  -->

<div align="center">

![](https://qcloudimg.tencent-cloud.cn/raw/8349ac97b261279606316331488784c3.png)

 - SDKAppID: The ID of an IM application. You cannot make a call across applications.
 - Secretkey: The key of an IM application, which you will use in step 5. The key and `SDKAppID` are used to generate `UserSig`, which is required for authentication.

## Step 2: Integrate TUICallKit

### Method 1: Integrate using npm

Download the `TUICallKit` component using npm. In case you need to scale your business in the future, we recommend you copy `TUICallKit` to the `src/components/` directory of your project.

```bash
# macOS
yarn add @tencentcloud/call-uikit-vue  # If you haven’t installed Yarn, execute `npm install -g yarn` first.
mkdir -p ./src/components/TUICallKit/Web && cp -r ./node_modules/@tencentcloud/call-uikit-vue/* ./src/components/TUICallKit/Web

# Windows
yarn add @tencentcloud/call-uikit-vue  # If you haven’t installed Yarn, execute `npm install -g yarn` first.
xcopy .\node_modules\@tencentcloud\call-uikit-vue  .\src\components\TUICallKit\Web /i /e
```

### Method 2: Integrate the source code

1. Download the `TUICallKit` source code from [GitHub](https://github.com/tencentyun/TUICallKit/tree/main/Web) and copy the `TUICallKit/Web` folder to the `src/components` folder of your project.

<!-- <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/e4699aaa507aa4618034463225f72cb2.png"/>  -->

<div align="center">

<img style="width:300px; max-width: inherit;" src="https://user-images.githubusercontent.com/57169560/194735247-3cbe30c6-37ab-43a4-97f0-27b8e40140cf.png"/> 
</div>

2. Go to the above folder and install the required dependencies.
```shell
cd ./src/components/TUICallKit/Web 
yarn         # If you haven’t installed Yarn, execute `npm install -g yarn` first.
```

## Step 3. Call `TUICallKit`

Call `TUICallKit` on a page to show the call view.

1. Import the UI. Below is an example:

```js
<script lang="ts" setup>
import { TUICallKit } from "./components/TUICallKit/Web";
</script>
  
<template>
  <TUICallKit />
</template>
```

2. Log in and make a call.

   2.1 If you are already using a [TUIKit](https://www.tencentcloud.com/document/product/1047/50061) component, add the code below to declare `TUICallKit` as a plugin. If you are not already using a TUIKit component, skip this.

   ```javascript
   import { TUICallKit } from './components/TUICallKit/Web';
   TUIKit.use(TUICallKit); 
   ```

   2.2 Initialize the component before making a call.

   ```javascript
   import { TUICallKitServer } from './components/TUICallKit/Web';
   TUICallKitServer.init({ SDKAppID, userID, userSig }); 
   ```

   >? 
   >- For how to get the `SDKAppID` and `SecretKey`, see step 1.
   > **As a temporary method**, you can use `genTestUserSig(userID)` in `GenerateTestUserSig.js` to generate `userSig`:
   >```javascript
   >import * as GenerateTestUserSig from "./components/TUICallKit/Web/demos/basic/public/debug/GenerateTestUserSig.js";
   >const { userSig } = GenerateTestUserSig.genTestUserSig(userID, SDKAppID, SecretKey);
   >```
   >- If you use Vite to start your project, you also need to perform [these steps](#2-Vite import).
   
   >! In this document, the method to obtain `UserSig` is to configure a `SECRETKEY` in the client code. In this method, the `SECRETKEY` is vulnerable to decompilation and reverse engineering. Once your `SECRETKEY` is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running and debugging a demo project**. The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).
   
    2.3 Run the following code where call making needs to be implemented:
   
    ```javascript
    import { TUICallKitServer } from './components/TUICallKit/Web';
    TUICallKitServer.call({ userID: "123", type: 2 }); // One-to-one call
    TUICallKitServer.groupCall({ userIDList: ["xxx"], groupID: "xxx", type: 2 }); // Group call
    ```

    You can now make your first call. For information on API parameters, see [API Documentation](https://www.tencentcloud.com/document/product/647/51015).

3. Advanced APIs

`TUICallKit` offers the `beforeCalling` and `afterCalling` callbacks to send you notifications about call status.

- `beforeCalling`: Returned before a call.
- `afterCalling`: Returned after a call.

For example, you can use them to expand and collapse the `<TUICallKit />` component (as shown in the [demo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/src/App.vue)).

```javascript
function beforeCalling() {
  console.log("This is executed before a call.");
}
function afterCalling() {
  console.log("This is executed after a call.");
}
```

```html
<TUICallKit :beforeCalling="beforeCalling" :afterCalling="afterCalling"/>
```

## Related documents

- [TUICallKit](https://www.tencentcloud.com/document/product/647/51015)
- [TUICallKit basic demo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md)
- [UI Customization (TUICallKit)](https://www.tencentcloud.com/document/product/647/50997)
- [FAQs (Web)](https://www.tencentcloud.com/document/product/647/51024)

## FAQs
### 1. How do I generate a UserSig?

The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide a project-oriented API. When `UserSig` is needed, your project can send a request to your server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

### 2. Vite import

If you created your project using Vite, because Vite uses a different file packaging method, you need to import `lib-generate-test-usersig.min.js` in `index.html`.

```javascript
// index.html
<script src="./src/components/TUICallKit/Web/demos/basic/public/debug/lib-generate-test-usersig.min.js"> </script>
```

Comment out the import method in `GenerateTestUserSig.js`.

```javascript
// import * as LibGenerateTestUserSig from './lib-generate-test-usersig.min.js'
```

### 3. Environment requirements

#### Browser versions

We recommend you use the latest version of Chrome. The table below shows the support for `TUICallKit` by mainstream browsers:

<table>
<thead><tr><th>OS</th><th> Browser</th><th>Minimum Browser Version Requirement</th></tr></thead>
<tbody><tr>
<td>macOS</td>
<td>Safari (desktop)</td>
<td>11+</td>
</tr><tr>
<td>macOS</td>
<td>Chrome (desktop)</td>
<td>56+</td>
</tr><tr>
<td>macOS</td>
<td>Firefox (desktop)</td>
<td>56+</td>
</tr><tr>
<td>macOS</td>
<td>Edge (desktop)</td>
<td>80+</td>
</tr><tr>
<td>Windows</td>
<td>Chrome (desktop)</td>
<td>56+</td>
</tr><tr>
<td>Windows</td>
<td>QQ Browser (desktop, WebKit core)</td>
<td>10.4+</td>
</tr><tr>
<td>Windows</td>
<td>Firefox (desktop)</td>
<td>56+</td>
</tr><tr>
<td>Windows</td>
<td>Edge (desktop)</td>
<td>80+</td>
</tr>
</tbody></table>

>? For more information on browser compatibility, see [Browsers Supported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html). You can also run an online test using the [TRTC compatibility check page](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html).

#### Network

Audio/Video calls may fail due to firewall restrictions. To avoid this, add the [ports and domain names](https://intl.cloud.tencent.com/document/product/647/35164) used by `TUICallKit` to your firewall’s allowlist.

#### Website domain protocol

For security and privacy reasons, only HTTPS URLs can access all features of the component. Please use the HTTPS protocol for your website in production environments.

<table>
<thead><tr><th>Scenario</th><th>Protocol</th><th>Receive (Playback)</th><th>Send (Publish)</th><th>Share Screen</th><th>Remarks</th></tr></thead>
<tbody><tr>
<td>Production</td>
<td>HTTPS</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Recommended</td>
</tr><tr>
<td>Production</td>
<td>HTTP</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr><tr>
<td>Local development</td>
<td>http://localhost</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Recommended</td>
</tr><tr>
<td>Local development</td>
<td>http://127.0.0.1</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr><tr>
<td>Local development</td>
<td>http://[local IP]</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr><tr>
<td>Local development</td>
<td align="left">file:///</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr>
</tbody></table>