This document describes how to quickly integrate the `TUICallKit` component. Performing the following key steps generally takes about an hour, after which you can implement the video call feature with complete UIs.

To try out the component, see [TUICallKit basic demo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md).

Before integration, check whether your desktop browser supports the audio/video services. For more information, see [Environment Requirements](https://www.tencentcloud.com/document/product/647/50993#1b83cb8f-4c54-43f3-863d-579786ab78bc).

[](id:step1)
## Step 1. Activate the service

`TUICallKit` is an audio/video call component developed based on two paid PaaS services: [IM](https://intl.cloud.tencent.com/document/product/1047/35448) and [TRTC](https://intl.cloud.tencent.com/document/product/647/35078). You can activate the services and enjoy a 60-day free trial as follows:

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click **Create Application**. In the pop-up window, enter your application name and click **OK**.
![img](https://qcloudimg.tencent-cloud.cn/raw/ce2e34f7cd1cd14679fc5decffb469af.png)

2. Click the application you just created to enter the **Basic Configuration** page. In the **Tencent Real-Time Communication** area at the bottom right of the page, click **Try now**. In the pop-up window, click **Activate now** to activate a 60-day free trial of `TUICallKit`.
![img](https://qcloudimg.tencent-cloud.cn/raw/796e49d9f55174aacb62bb8eb848feaf.png)

3. On the same page, find and record the **SDKAppID** and **Key**, which will be used in subsequent steps.
	![img](https://qcloudimg.tencent-cloud.cn/raw/8349ac97b261279606316331488784c3.png)
	- `SDKAppID`: The IM application ID, which is used for business isolation; that is, calls with different `SDKAppID` values cannot be interconnected.
	- `Secretkey`: The IM application key, which needs to be used together with `SDKAppID` to generate the authentication credential `UserSig` for authorized use of IM. It will be used in step 5.

[](id:step2)
## Step 2. Import the `TUICallKit` component

1. Download the `TUICallKit` source code from [GitHub](https://github.com/tencentyun/TUICallKit/tree/main/Web) and copy the `TUICallKit/Web` folder to the `src/components` folder of your project.
![img](https://qcloudimg.tencent-cloud.cn/image/document/b90fbef92c17090688ebc0c9b4577037.png)

1. Enter the folder and install required dependencies.
```shell
cd ./src/components/TUICallKit/Web 
yarn                                  // If Yarn isn't installed in the current environment, you can run `npm install -g yarn` to install it.
```

[](id:step3)
## Step 3. Generate `UserSig`

If `UserSig` has been generated, you can skip this step and proceed to [step 4](#step4).

1. Set initialization parameters, where `SDKAppID` and `Key` can be obtained in the [IM console](https://console.tencentcloud.com/im). Click the card of the target application to enter its **Basic Configuration** page.
![img](https://qcloudimg.tencent-cloud.cn/raw/95ab37db3b8c371d7fa86af24b5a6aad.png)

2. In the **Basic info** section, click **Display key**, and copy and save the key information to the `TUICallKit/Web/demos/basic/public/debug/GenerateTestUserSig.js` file.
![img](https://qcloudimg.tencent-cloud.cn/raw/8cbbf4515e40f0e3bc0062b2c17a635e.png)

3. In step 4, you can use the `genTestUserSig(userID)` function in `GenerateTestUserSig.js` to calculate `userSig`.
```javascript
import * as GenerateTestUserSig from "../public/debug/GenerateTestUserSig.js";
const { userSig } = GenerateTestUserSig.genTestUserSig(userID);
```

4. If you use Vite for startup, pay attention to the [import issue in Vite](https://www.tencentcloud.com/document/product/647/50993#f020d04e-5439-4679-bc6e-716f7329b60a).

>! Before release, you must delete this file. In this document, the method to get `UserSig` is to configure a `SECRETKEY` in the client code. In this method, the `SECRETKEY` is vulnerable to decompilation and reverse engineering. Once your `SECRETKEY` is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running feature debugging**. The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://www.tencentcloud.com/document/product/1047/34385).

[](id:step4)
## Step 4. Call the `TUICallKit` component

You can call the `TUICallKit` component on the desired page to display the call page.

1. `TUICallKit` UI import
```js
<script lang="ts" setup>
import { TUICallKit } from "./src/components/TUICallKit/Web";
</script>
  
<template>
  <div class="call-kit-container">
    <TUICallKit />
  </div>
</template>
  
<style scoped>
.call-kit-container {
  width: 50rem;
  height: 35rem;
  border-radius: 16px;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
}
</style>
```

2. User login and call making
    2.1 If the [TUIKit](https://www.tencentcloud.com/document/product/1047/50061) kit has been used, you need to import the following code and declare `TUICallKit` as a plugin; otherwise, you don't need to import the following code:
  ```
    import { TUICallKit } from './src/components/TUICallKit/Web/src/index';
    TUIKit.use(TUICallKit);
  ```

  2.2 Run the following code where user login needs to be implemented:
  ```
    import { TUICallKitServer } from './src/components/TUICallKit/Web/src/index';
    TUICallKitServer.init({ SDKAppID, userID, userSig }); 
  ```
>? `userSig` can be obtained in [step 3](#step3).

  2.3 Run the following code where call making needs to be implemented:
	```
		import { TUICallKitServer } from './src/components/TUICallKit/Web/src/index';
		TUICallKitServer.call({ userID, type }); // One-to-one call
		TUICallKitServer.groupCall({ userIDList, groupID, type }); // Group call
	```
	After completing the above steps, you can make your first call successfully. For more information on the API parameters, see [API Documentation](https://www.tencentcloud.com/document/product/647/51015).

3. Advanced APIs
	This component provides the `beforeCalling` and `afterCalling` callbacks, which can be used to notify you of the current call status.
	- `beforeCalling`: Returned before a call.
	- `afterCalling`: Returned after a call.

For example, you can use them to expand and collapse the `<TUICallKit />` component as instructed in [TUICallKit/Web/demos/basic/src/App.vue](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/src/App.vue).
```javascript
function beforeCalling() {
  console.log("This function is executed before a call.");
}
function afterCalling() {
  console.log("This function is executed after a call.");
}
```
```javascript
<TUICallKit :beforeCalling="beforeCalling" :afterCalling="afterCalling"/>
```

## Other Documents

- [API Introduction](https://github.com/tencentyun/TUICallKit/blob/main/Web/docs/API.md)
- [TUICallKit basic demo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md)
- [TUICallKit UI Customization Guide](https://github.com/tencentyun/TUICallKit/blob/main/Web/docs/UI%20Customization.md)
- [FAQs (Web)](https://www.tencentcloud.com/document/product/647/51024)


## FAQs

### 1. How do I generate a UserSig?

The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide a project-oriented API. When `UserSig` is needed, your project can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://www.tencentcloud.com/document/product/1047/34385?lang=en&pg=).

### 2. Import issue in Vite

If you create your project in Vite, as Vite uses a different file packaging method, you need to import `lib-generate-test-usersig.min.js` into `index.html`.
```javascript
// index.html
<script src="/public/debug/lib-generate-test-usersig.min.js"> </script>
```

Comment out the imported method in `GenerateTestUserSig.js`.

```javascript
// import * as LibGenerateTestUserSig from './lib-generate-test-usersig.min.js'
```

### 3. Environment requirements

#### Requirements for the browser version

| OS | Browser (Desktop) | Minimum Browser Version Requirement |
| -------- | ---------------------------- | ------------------ |
|  macOS  |     Safari     |        11+         |
|  macOS  |     Chrome     |        56+         |
|  macOS  |    Firefox     |        56+         |
|  macOS  |      Edge      |        80+         |
| Windows  |     Chrome     |        56+         |
| Windows | QQ Browser (WebKit core) |      10.4+       |
| Windows  |    Firefox     |        56+         |
| Windows  |      Edge      |        80+         |

>?For more information on browser compatibility, see [Tutorial: Browsers Supported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html). You can also run an online test using the [TRTC compatibility check page](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html).

#### Requirements for the network environment

When using `TUICallKit`, a user may fail to have a normal audio/video call due to firewall restrictions. In this case, add the corresponding port and domain name to the firewall allowlist as instructed in [Firewall Restrictions](https://www.tencentcloud.com/document/product/647/35164).

#### Requirements for the website domain name protocol

For security and privacy reasons, only HTTPS URLs can access all features of the integrated component described in this document. To ensure that users in the production environment can use the product features properly, deploy your website under a domain name using the **HTTPS** protocol.

>! You can use `http://localhost` or `file://` URLs for local development.

The table below lists the supported domain names and protocols.

| Scenario     | Protocol             | Receive (Playback) | Send (Push) | Share Screen | Remarks |
| ------------ | ---------------- | ------------ | ------------ | -------- | ---- |
| Production     | HTTPS        | Supported         | Supported         | Supported     | Recommended |
| Production     | HTTP         | Supported         | Not supported       | Not supported   | -    |
| Local debugging | http://localhost | Supported         | Supported         | Supported     | Recommended |
| Local debugging | http://127.0.0.1 | Supported         | Supported         | Supported     | -    |
| Local debugging | http://[local IP address]  | Supported         | Not supported       | Not supported   | -    |
| Local debugging | file:/// | Supported         | Supported         | Supported     | -    |
