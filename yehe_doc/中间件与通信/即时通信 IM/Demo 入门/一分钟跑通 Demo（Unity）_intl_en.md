This document introduces how to quickly run through the IM demo (Unity).

## Environment Requirements

| Platform | Version |
|---------|---------|
| Unity | 2019.4.15f1 or later |
| Android | Android Studio 3.5 or later; devices with Android 4.1 or later for apps |
| iOS | Xcode 11.0 or later. Ensure that your project has a valid developer signature. |

## Prerequisites

You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
[](id:step1)
## Step 1: Create an App
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
 >? If you already have an app, record its SDKAppID and [obtain key information](#step2).
 > A Tencent Cloud account can create a maximum of 300 IM apps. If you want to create more apps, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first and then create a new one. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost. Proceed with caution**.
 >
2. Click **Create Application**, enter your app name, and click **Confirm**.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. After creation, you can see the status, service version, SDKAppID, creation time, and expiry time of the new app on the overview page of the console. Record the SDKAppID.
    ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. Click the created app. In the left sidebar, click **Auxiliary Tools** -> **UserSig Tools** to create a UserID and the corresponding UserSig. Then copy the UserSig for future login.
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)
## Step 2: Download the SDK and Source Code
1. Download the SDK and matching [demo source code](https://intl.cloud.tencent.com/document/product/1047/33996).
2. Double-click to open the downloaded package. Select all resources in the package (default) and import them to the current Unity project.
![](https://main.qcloudimg.com/raw/c338ce838fff81841f85b06fd3dc5c6c.png)
3. Open the source code file **ExampleEntry.cs** in **Assets** -> **TIMCloud** -> **Demo**, enter the SDKAppID, UserID, and UserSig obtained in [step 1](#step1) in the corresponding red boxes in the figure blow, and comment out the line where `Config.key` resides.
![](https://main.qcloudimg.com/raw/e31692ae98503221f45ece41039ead92.png)
4. Comment out the logic for dynamically getting the UserSig in `ExampleEntry.cs` (since the configuration of dynamic UserSig getting is complex, you can configure it separately later).
![](https://main.qcloudimg.com/raw/7a8ac734ac60a73caf6139fc0d1d250f.png)

## Step 3: Build and Run the Demo
### Android
1. Configure Unity Editor, click **File** -> **Build Settings**, and switch the platform to Android.
![](https://main.qcloudimg.com/raw/d913d32e36aa01ff93acf0316d4f103f.png)
2. Start an Android simulator and click **Build And Run** to run the demo.

>- The demo includes all activated APIs and can be used for testing and calling reference. For the API documentation, see [SDK API (Unity)](https://intl.cloud.tencent.com/document/product/1047/40125).
> - The UI may have certain changes. Please refer to the latest version.
>
![](https://main.qcloudimg.com/raw/e6f3583d0b807af62a27ee753cfa3b53.png)
3. Test APIs: enter your UserID in the second text box in the first row, and call `initSDK` and `login`. The data display window indicates that the call is successful. Then you can call the remaining APIs.

### iOS
1. Configure Unity Editor, click **File** -> **Build Settings**, and switch the platform to iOS.
![](https://main.qcloudimg.com/raw/3982b96c4f9e76107bb4aadac33a5de5.png)
2. Connect to a real iPhone, and click **Build And Run**. You need to select a new folder to save your iOS build. When the build is completed, the folder containing the Xcode project will open in a new window.
3. Open the iOS project and set **Signing & Capabilities** for the main target (with an Apple developer account required) to enable the project to run on an iPhone device.
4. Start the project and debug the demo on the iPhone device.

## FAQs

### What platforms are supported?
Currently, both iOS and Android platforms are supported. In addition, the editions for Windows and Mac are under development. Please stay tuned.

### What should I do if Android reports an error where no available device can be found when I click **Build And Run**?
Check that the device is not occupied by other resources. Or click **Build** to generate an APK package, drag it to the simulator, and run it.

### What should I do if iOS reports an error during the first run?
If iOS reports an error after the demo configured as above is run, click **Product** -> **Clean**, clean the product, and build the demo again. You can also close Xcode and open it again, and then build the demo again.
### What should I do if Unity v2019.04 on iOS reports the following error?
Library/PackageCache/com.unity.collab-proxy@1.3.9/Editor/UserInterface/Bootstrap.cs(23,20): error CS0117: 'Collab' does not contain a definition for 'ShowChangesWindow'
Click **Window** > **Package Manager** on the Editor toolbar to downgrade Unity Collaborate to 1.2.16.

### What should I do if Unity v2019.04 on iOS reports the following error?
Library/PackageCache/com.unity.textmeshpro@3.0.1/Scripts/Editor/TMP_PackageUtilities.cs(453,84): error CS0103: The name 'VersionControlSettings' does not exist in the current context
Open the source code and delete the code snippet of `|| VersionControlSettings.mode != "Visible Meta Files"`.
