This document describes how to quickly run the Tencent Cloud TRTC Demo for Android.

## Environment Requirements
- Compatibility with Android 4.1 (SDK API Level 16) or above is required. Android 5.0 (SDK API Level 21) or above is recommended.
- Android Studio 3.5 or above.
- Device on Android 4.1 or above for the application.

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name such as `TestTRTC`, and click **Create Application**.

<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the card, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Android)** to go to the GitHub website (or click **[ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip?_ga=1.195966252.185644906.1567570704)**) to download the SDK and supporting demo source code.
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.


<span id="step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `LiteAVSDK_TRTC_Android_version number/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` file.
3. Set the relevant parameters in the `GenerateTestUserSig.java` file:
  <ul><li>SDKAPPID: it is `PLACEHOLDER` by default. Please replace it with the real `SDKAppID`.</li>
  <li>SECRETKEY: it is `PLACEHOLDER` by default. Please replace it with the real key information.</li></ul> 
	<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage application.

>!In this document, the `SECRETKEY` is configured in the client code to obtain `UserSig`. The `SECRETKEY` is easily decompiled and reverse cracked. If the `SECRETKEY` is leaked, hackers can steal your Tencent Cloud traffic. Therefore, **this method only applies to locally running a demo project and commissioning features**.
>The correct `UserSig` distribution method is to integrate the computing code of `UserSig` into your server and provide an app-oriented API. When `UserSig` is needed, your app can send a request to the business server to obtain the dynamic `UserSig`. For more information, see [How to Generate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Compile and run
Use Android Studio (v3.5 or above) to open the `TRTCScenesDemo` project and click **Run**.

## FAQs
### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to upgrade the signature algorithm before you can get a new encryption key. If you don’t upgrade it, you can continue to use the [legacy algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). If you have upgraded the version, you can switch between the new and old algorithms as needed.

Upgrade/switch the algorithm as follows:
 1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc).
 2. Select **Application Management** on the left sidebar and click **Application Info** on the row of the target application.
 3. Select the **Quick Start** tab and click **upgrade**, **asymmetric encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade:

  - Switch to the legacy algorithm ECDSA-SHA256:
   ![](https://main.qcloudimg.com/raw/a8737123c1e3cc0f7eb34901ed2629f7.png)
  - Switch to the new algorithm HMAC-SHA256:
   ![](https://main.qcloudimg.com/raw/701fcde1a562bf9fbbb0d426948e311e.png)

### 2. The demo is running on two mobile phones, but why can't they display the images of each other?
Please make sure that the two mobile phones use different `UserIDs` when running the demo, as TRTC does not support using the same `UserID` on two devices simultaneously; unless different `SDKAppIDs` are used.


### 3. What are the restrictions of the firewall?
As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please troubleshoot as instructed in [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).
