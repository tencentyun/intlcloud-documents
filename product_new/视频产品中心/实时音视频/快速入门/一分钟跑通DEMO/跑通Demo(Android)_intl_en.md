This document describes how to quickly run the Tencent Cloud TRTC Demo for Android.

## Environment Requirements
- Compatibility with Android 4.1 (SDK API Level 16) or above is required. Android 5.0 (SDK API Level 21) or above is recommended
- Android Studio 2.0 or above
- Device on Android 4.1 or above for the application

## Prerequisites
You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and [verified your identity](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the [TRTC Console](https://console.cloud.tencent.com/rav).
 - If you are logging in for the first time, click **Start Now** directly.
  ![](https://main.qcloudimg.com/raw/063eb714daa9ab9076b20663bd4c78b7.png)
 - Otherwise, click **+ Create Application and Run Demo** and then click **Start Now**.
  ![](https://main.qcloudimg.com/raw/fb5ca0967f09d4970b2dc610f17d5b2c.png)
2. Enter the application name and click **Create Application**.
 ![](https://main.qcloudimg.com/raw/da7b1535b37c4d0b3e63ce49598149fe.png)

<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the "Android" card, click **[GitHub](https://github.com/tencentyun/TRTCSDK)** to redirect to GitHub (or click **[ZIP](https://gitee.com/cloudtencent/TRTCSDK)**) and download the relevant SDK and auxiliary demo source code.
  ![](https://main.qcloudimg.com/raw/363243119b9faf74f8585ee08d01e5a9.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**.

<span id="step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#step2). Find and open the `Android/TRTCDemo/app/src/main/java/com/tencent/liteav/demo/trtc/debug/GenerateTestUserSig.java` file and configure the following parameters:
  - SDKAPPID: set to the corresponding **SDKAppID**.
  - SECRETKEY: set to the corresponding **key**.
  ![](https://main.qcloudimg.com/raw/7f1c7345b4019984553fae9480fde461.png)
2. Return to the TRTC Console and click **Pasted and Next**.
3. Click **Close Guide and Enter Console** to manage application.

>!The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Server-side UserSig Generation](https://intl.cloud.tencent.com/document/product/647/35166#Server).

### Step 4. Compile and run
Use Android Studio (v3.2 or above) to open the `TRTCDemo` project and click **Run**.

## FAQs

### 1. The demo is running on two mobile phone, but why can't they display the images of each other?
Please make sure that the two mobile phones use different `UserIDs` when running the demo, as TRTC does not support using the same `UserID` on two devices simultaneously; unless different `SDKAppIDs` are used.
![](https://main.qcloudimg.com/raw/c7b1589e1a637cf502c6728f3c3c4f99.png)

### 2. What are the restrictions of the firewall?
As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please troubleshoot as instructed in [Dealing with Organizational Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).
