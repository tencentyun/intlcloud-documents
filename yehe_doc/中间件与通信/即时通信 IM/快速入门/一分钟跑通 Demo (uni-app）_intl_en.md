Tencent Cloud IM officially launched the application that allows you to compile Android and iOS apps in HBuilder X based on the Web IM SDK and package a set of code on multiple clients.

## Online Customer Service Scenario
The demo provides basic templates for sample customer service groups and sample friends. Features for the online customer service scenario include:
- Sending common messages such as text, image, voice, and video messages
- Supporting custom messages such as commonly used expressions, orders, service evaluation messages
- Creating group chat conversations and managing group members


## Directions
### Step 1. Register and create a uni-app account
1. Build the app development environment. Please download [HBuilder X](https://www.dcloud.io/hbuilderx.html).
>!Currently, the latest version of HBuilder X is used in the project. If you have downloaded HBuilder X before, please update it to the latest version to ensure a unified development environment.
2. Register in the [DCloud Developer Center](https://dev.dcloud.net.cn/) and log in to HBuilder X.

### Step 2. Create an app
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
>?
>- If you already have an app, record its SDKAppID and [obtain key information](#step2).
>- A Tencent Cloud account can create a maximum of 300 IM apps. If you want to create more apps, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first and then create a new one. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost. Proceed with caution**.
>
2. Click **Create Application**, enter your app name, and click **Confirm**.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. After creation, you can see the status, service version, SDKAppID, creation time, and expiry time of the new app on the overview page of the console. Record the SDKAppID.
    ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. Click the created app. In the left sidebar, click **Auxiliary Tools** -> **UserSig Tools** to create a UserID and the corresponding UserSig. Then copy the UserSig for future login.
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)
>! Please store the key information properly to prevent leakage.

### Step 3. Download and configure the uni-app source code
1. Download the SDK and matching [demo source code](https://intl.cloud.tencent.com/document/product/1047/33996).
```javascript
# Run in CLI
git clone https://github.com/tencentyun/TIMSDK.git

# Enter the uni-app TUIKit project
cd TIMSDK/uni-app/TUIKit
```
2. Import the uni-app TUIKit project file to your HBuilder X project (version 3.2.11.20211021-alpha). For more information, please see [Creating uni-app](https://uniapp.dcloud.io/quickstart-hx).
3. Set relevant parameters in the `GenerateTestUserSig` file:
- Find and open the `debug/GenerateTestUserSig.js` file.
- Set parameters in the `GenerateTestUserSig.js` file as follows:
  <ul><li>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.</li>
  <li>SECRETKEY: left empty by default. Set it to the actual key.</li></ul> 
  

>! 
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the uni-app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Compile and run
See [Running uni-app](https://uniapp.dcloud.io/quickstart-hx?id=%e8%bf%90%e8%a1%8cuni-app).

### Step 5. Package and publish

 See [Packaging uni-app](https://uniapp.dcloud.io/quickstart-hx?id=%e5%8f%91%e5%b8%83uni-app).
- Native App - Cloud packaging: **HBuilderX** > **Publish** > **Native App** - **Cloud packaging** (Detailed settings such as the app icon and startup page can be configured in `manifest.json`.)
- Native App - Offline packaging: **HBuilderX** > **Publish** > **Generate local packaged app resource** (For the detailed packaging scheme, please see the iOS and Android local packaging guide.)

## FAQs
[](id:Q1)
### 1. uni-app supports Android and iOS. How do I choose for IM SDK?
Please select `tim-wx-sdk` and install it via npm or static import:
```javascript
    // SDK v2.11.2 and later versions support WebSocket, and you are advised to integrate such SDK versions. SDK v2.10.2 and earlier versions use HTTP.
	npm install tim-wx-sdk@2.15.0 --save
	import TIM from 'tim-wx-sdk';
	// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
	uni.$TUIKit = TIM.create({
		SDKAppID: 0 // Replace 0 with the SDKAppID of your IM application when connecting
	});
	
	// Set the SDK log output level. For details on each level, see **setLogLevel API description**.
	uni.$TUIKit.setLogLevel(0); // Common level. You are advised to use this level during access as it covers more logs.
	// uni.$TUIKit.setLogLevel(1); // Release level, at which the SDK outputs important information. You are advised to use this log level in a production environment.
```
If your project needs the relationship chain feature, please use `tim-wx-friendship.js`.
```javascript
	import TIM from 'tim-wx-sdk/tim-wx-friendship.js';
```
>?
>- **To allow uni-app better access and use TIM to quickly locate and resolve problems, do not change the name of uni.$TUIKit. If you have accessed TIM, please change uni.tim to uni.$TUIKit.**
>- Please upgrade IM SDK to [2.15.0](https://intl.cloud.tencent.com/document/product/1047/34281), which supports iOS voice message playback.
>- If a problem occurs during dependency synchronization, change the npm source and try again.
```javascript
	Change the cnpm source
	>npm config set registry http://r.cnpmjs.org/
	>
	>
```

[](id:Q2)
### 2. How do I upload rich media messages such as image, video, and voice messages?
Please use `cos-wx-sdk-v5`:
```javascript
    // The cos-wx-sdk-v5 upload plug-in is required to send rich media messages such as image, video, and voice messages.
	npm install cos-wx-sdk-v5@0.7.11 --save
	import COS from "cos-wx-sdk-v5";
	// Register the COS SDK plugin.
	uni.$TUIKit.registerPlugin({
		'cos-wx-sdk': COS
	});
```

[](id:Q3)
### 3. Voice message playback in iOS built by uni-app failed. What should I do?
  Please upgrade IM SDK to [2.15.0](https://intl.cloud.tencent.com/document/product/1047/34281), which supports iOS voice message playback.

[](id:Q4)
### 4. The voice message sending time is displayed incorrectly in apps built by uni-app. What should I do?
   For apps built by uni-app, the `recorderManager.onStop` callback does not include the `duration` and `fileSize` fields, and you need to add the fields yourself.
- **Calculate the duration according to the time recorded by the local timer.**
- **Estimate the file size via local calculation: fileSize = Audio bitrate x Duration (unit: seconds) / 8**
For the detailed code, please see [uni-app TUIKit](https://github.com/tencentyun/TIMSDK/tree/master/uni-app).
>!
>
>- A voice message object must include the `duration` and `fileSize` fields. If `fileSize` is missing, the voice message duration will be a string of incorrect digits.

[](id:Q5)
### 5. A video message cannot be scrolled because its path contains too many levels. What should I do?
 Use video images instead of directly rendering the video in your project and render the video during playback to avoid the problem of excessive hierarchy.
 For the detailed code, please see [uni-app TUIKit](https://github.com/tencentyun/TIMSDK/tree/master/uni-app).
>!See [Native Component Description](https://uniapp.dcloud.io/component/native-component).

[](id:Q6)

### 6. A system error indicating an excessive size is reported during preview on a real machine. What should I do?
Select code compression at runtime: mini program simulator > whether to compress code at runtime

[](id:Q7)



## Technical Consultation
[Contact us](https://intl.cloud.tencent.com/zh/contact-us).

## Reference Documents

- [SDK API Documentation](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html)
- [SDK Update Log](https://intl.cloud.tencent.com/document/product/1047/34281)
- [uni-app TUIKit Source Code](https://github.com/tencentyun/TIMSDK/tree/master/uni-app)
- [Quick Integration of uni-app TUIKit Source Code](https://intl.cloud.tencent.com/document/product/1047/43893)

