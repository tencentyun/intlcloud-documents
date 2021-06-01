This document describes how to quickly run the Tencent Cloud TRTC demo for iOS and macOS.

## Environment Requirements
- Xcode 11.0 or above
- Your project has a valid developer signature.
- Qt Creator 4.13.3 (macOs) or above

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
<span id="step1"></span>
### Step 1. Create an application.
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name, e.g. `TestTRTC`, and click **Create**.

<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding block to download the SDK and demo source code.
### iOS
- **iOS:** click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)** to visit GitHub (or click **[ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip?_ga=1.195966252.185644906.1567570704)**)
![](https://main.qcloudimg.com/raw/d7b68212e6e63e81c1e0a19e1236a4b3/%E8%B7%91%E9%80%9ADemoiOS&Mac1-%E8%BF%94%E8%BF%98.png)

- **macOS:** click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Mac)** to visit GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2?_ga=1.195966252.185644906.1567570704)**)
    ![](https://main.qcloudimg.com/raw/9f1ca4547228695031845d049dd7755d/%E8%B7%91%E9%80%9ADemoiOS&Mac2-%E8%BF%94%E8%BF%98.png)

2. After the download, return to the TRTC console and click **Downloaded and Next** to view your `SDKAppID` and secret key.

<span id="step3"></span>
### Step 3. Configure demo project files.
1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `GenerateTestUserSig.h` file.
 <table><tr>
<th nowrap="nowrap">Platform</th><th nowrap="nowrap">Relative Path to File</th></tr>
<tr>
<td>iOS</td><td>iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h</td>
</tr><tr>
<td>Mac</td><td>Mac/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h</td>
</tr></table>
3. Set parameters in the `GenerateTestUserSig.h` file.
  <ul><li>SDKAPPID: it is 0 by default. Please replace it with the real `SDKAppID`.</li>
  <li>SECRETKEY: left empty by default. Set it to the actual secret key.</li></ul> 

4. Return to the TRTC console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console to Manage Applications**.

>!The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Compile and run the project.
1. Go to the directory where the `TRTCScenesDemo > Podfile` file of the source code is located in a terminal window.
2. Run the `pod install` command to install the TRTC SDK, or run the `pod update` command to update the local library.
3. Use Xcode (11.0 or above) to open the `TXLiteAVDemo.xcworkspace` project in the source code directory, and compile and run the project.

## FAQ

### 1. Only public and private key information can be obtained when I try to view the secret key. How do I get the secret key?
TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new secret key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** on the left sidebar, find the target application, and click **Application Info**.
 3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade:
  - Switch to the legacy algorithm ECDSA-SHA256:
      ![](https://main.qcloudimg.com/raw/bc5cc756b93bd3e688f9f31a9c1efdfe/%E8%B7%91%E9%80%9ADemo(iOS&Mac)5-%E8%BF%94%E8%BF%98.png)
  - Switch to the new algorithm HMAC-SHA256.
      ![](https://main.qcloudimg.com/raw/2f55ac47bbff3257bfadc7e670e0ff1c/%E8%B7%91%E9%80%9ADemo(iOS&Mac)6-%E8%BF%94%E8%BF%98.png)

### 2. The demo is running on two mobile phones, but why can't they display the images of each other?
Make sure that the two mobile phones use different `UserIDs`. With TRTC, you cannot use the same `UserID` on two devices simultaneously unless the `SDKAppIDs` are different.

### 3. What firewall restrictions does the SDK face?
The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) for assistance.
