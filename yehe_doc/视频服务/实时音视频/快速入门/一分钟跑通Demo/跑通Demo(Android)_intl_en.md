This document describes how to quickly run the Tencent Cloud TRTC Demo for Android.

## Environment Requirements
- Compatibility with Android 4.1 (SDK API Level 16) or above is required. Android 5.0 (SDK API Level 21) or above is recommended
- Android Studio 3.5 or above
- Device on Android 4.1 or above for the application

## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name such as `TestTRTC`, and click **Create Application**.

<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding card, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Android)** to redirect to GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip?_ga=1.195966252.185644906.1567570704)**) and download the relevant SDK and supporting demo source code.

2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.


<span id="step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` file.
3. Set the relevant parameters in the `GenerateTestUserSig.java` file:
  <ul><li>SDKAPPID: it is 0 by default. Please replace it with your real `SDKAppID`.</li>
  <li>SECRETKEY: it is an empty string by default. Please replace it with your real key information.</li></ul> 
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage the application.

>The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Server-Side UserSig Generation](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Compile and run
Use Android Studio (v3.5 or above) to open the `TRTCDemo` project and click **Run**.

## FAQs
### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to upgrade the signature algorithm before your can get a new encryption key. If you don't upgrade it, you can continue to use the [legacy algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166).

Upgrade operation:
 1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc).
 2. Select **Application Management** on the left sidebar and click **Application Info** on the row of the target application.
 3. Select the **Quick Start** tab and click **Upgrade** in **Step 2: obtain the secret key to issue UserSig**.

### 2. The demo is running on two mobile phone, but why can't they display the images of each other?
Please make sure that the two mobile phones use different `UserID` values when running the demo, as TRTC does not support using the same `UserID` on two devices simultaneously, unless different `SDKAppID` values are used.


### 3. What are the restrictions of the firewall?
As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please troubleshoot as instructed in [How to Deal With Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).
