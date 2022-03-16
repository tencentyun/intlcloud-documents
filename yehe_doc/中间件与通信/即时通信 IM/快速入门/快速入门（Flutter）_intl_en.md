This document describes how to quickly run the IM demo for Flutter.

## Environment Requirements

| Platform | Version |
|---------|---------|
| Flutter | 2.2.0 or later|
| Android | Android Studio 3.5 or later; devices with Android 4.1 or later for apps |
| iOS | Xcode 11.0 or later. Ensure that your project has a valid developer signature. |

## Prerequisites

You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
[](id:step1)

### Step 1. Create an app
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
>? If you already have an app, record its SDKAppID and [obtain key information](#step2).
>A Tencent Cloud account can create a maximum of 300 IM apps. If you want to create a new app, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost. Proceed with caution**.
>
2. Click **Create Application**, enter your app name, and click **Confirm**.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. After creation, you can see the status, service version, SDKAppID, creation time, and expiry time of the new app on the overview page of the console. Record the SDKAppID.
    ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. Click the created app. In the left sidebar, click **Auxiliary Tools** > **UserSig Tools** to create a UserID and the corresponding UserSig. Then copy the UserSig for future login.
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)
### Step 2. Download the SDK and source code
1. Download the SDK and [demo source code](https://github.com/tencentyun/TIMSDK/tree/master/Flutter/Demo/im_discuss) that fit your needs.
2. Then, go to the directory TIMSDK/Flutter/Demo/im_discuss.
![](https://qcloudimg.tencent-cloud.cn/raw/8b865854e14e8848b4e8d31d8daf55ac.png)
3. Run `Flutter pub get` to install the dependencies, launch the demo project, and enter the following command:
<dx-codeblock>
:::  plaintext
flutter run --dart-define=SDK_APPID=xxxx --dart-define=ISPRODUCT_ENV=false --dart-define=KEY=xxxx
:::
</dx-codeblock>
>?
>-  Replace `xxxx` in `--dart-define=SDK_APPID=xxxx` with the SDKAppID created in [Step 1](#step1).
>-  Use `--dart-define=ISPRODUCT_ENV=false` to determine the environment (development or production). Enter “false” for a development environment.
>-  Replace `xxxx` in `--dart-define=KEY=xxxx` with the key mentioned in [Step 1](#step1).
4. Configure the launch.json file in the Visual Studio.
![](https://qcloudimg.tencent-cloud.cn/raw/e495955902c8a594085aa045891ffe2a.png)


### Step 3 (optional). Run and debug the project in the IDE
<dx-tabs>
::: Android[](id:android)
1. Go to the discuss/andorid directory via Android Studio.
![](https://qcloudimg.tencent-cloud.cn/raw/6516f9b17c58915c4ebc93c5c8829831.png)
2. Start an Android simulator, tap **Build And Run** to run the demo. Enter a random UserID (a combination of digits and letters).
>? The UI of the latest version of the demo may look different after adjustments.
:::
::: iOS[](id:ios)
1. Open Xcode and the file discuss/ios/Runner.xcodeproj:
![](https://qcloudimg.tencent-cloud.cn/raw/6d74814ba9bce54c7439e8b3cea53e73.png)
2. Connect an iPhone, and click **Build And Run**. After the iOS project is built, the Xcode project will be displayed in a new pop-up window.
3. Open the iOS project, and set **Signing & Capabilities** (an iPhone developer account required) for the primary target to run the project on the iPhone.
4. Start the project and debug the demo on the iPhone device.
![](https://qcloudimg.tencent-cloud.cn/raw/3fe6bbac88bb21ad7a7822bb297793b3.png)
:::
</dx-tabs>

## FAQs

### What platforms are supported?
Currently, iOS, Android, and web platforms are supported. In addition, the editions for Windows and macOS are under development. Please stay tuned.

### What should I do if clicking **Build And Run** for an Android device triggers an error, stating no available device is found?
Check that the device is not occupied by other resources. Alternatively, click **Build** to generate an APK package, drag it to the simulator, and run it.

### What should I do if an error occurs during the first run for an iOS device?
If an error is reported for an iOS device after the demo configured as above is run, choose **Product** > **Clean** to clean the product, and build the demo again. You can also close Xcode and open it again, and then build the demo again.

### Flutter environment
If you want to check the Flutter environment, run `Flutter doctor` to detect whether the Flutter environment is ready.
