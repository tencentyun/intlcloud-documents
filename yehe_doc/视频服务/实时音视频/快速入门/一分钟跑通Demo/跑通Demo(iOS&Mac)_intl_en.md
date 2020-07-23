This document describes how to quickly run the Tencent Cloud TRTC Demo for iOS and macOS.

## Environment Requirements
- Xcode 11.0 or above
- Make sure that your project has a valid developer signature

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name such as `TestTRTC`, and click **Create Application**.

<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the block to download the SDK and supporting demo source code.
 - **iOS:** click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)** to go to the GitHub website (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip?_ga=1.195966252.185644906.1567570704)**)
  ![](https://main.qcloudimg.com/raw/716b5af9207ad2b11835dec4e2d15da0.png)
 - **macOS:** click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Mac)** to go to the GitHub website (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2?_ga=1.195966252.185644906.1567570704)**)
  ![](https://main.qcloudimg.com/raw/65b9538a23789b1a728674ea3646062c.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

<span id="step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `GenerateTestUserSig.h` file:
 <table><tr>
      <th nowrap="nowrap">Platform</th>
      <th nowrap="nowrap">Relative Path to File</th>
  </tr>
<tr>
      <td>iOS</td>
<td>iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h</td>
  </tr>
<tr>
    <td>macOS</td>
    <td>Mac/TRTCScenesDemo/TRTCDemo/TRTC/GenerateTestUserSig.h</td>
  </tr></table>
3. Set the relevant parameters in the `GenerateTestUserSig.h` file:
  <ul><li>SDKAPPID: it is 0 by default. Please replace it with the real `SDKAppID`.</li>
  <li>SECRETKEY: it is an empty string by default. Please replace it with the real key information.</li></ul> 
	<img src="https://main.qcloudimg.com/raw/15d986c5f4bc340e555630a070b90d63.png">
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage application.

>In this document, the `SECRETKEY` is configured in the client code to obtain `UserSig`. The `SECRETKEY` is easily decompiled and reverse cracked. If the `SECRETKEY` is leaked, hackers can steal your Tencent Cloud traffic. Therefore, **this method only applies to locally running a demo project and commissioning features**.
>The correct `UserSig` distribution method is to integrate the computing code of `UserSig` into your server and provide an app-oriented API. When `UserSig` is needed, your app can send a request to the business server to obtain the dynamic `UserSig`. For more information, see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Compile and run
1. Enter the directory where the `TRTCSimpleDemo > Podfile` file is located in a terminal window.
2. Run the `pod install` command to install the TRTC SDK, or run the `pod update` command to update the local library.
3. Use Xcode (v11.0 or above) to open the `TXLiteAVDemo.xcworkspace` project in the source code directory, compile it, and run the demo project.

## FAQs

### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to upgrade the signature algorithm before you can get a new encryption key. If you don’t upgrade it, you can continue to use the [legacy algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). If you have upgraded the version, you can switch between the new and old algorithms as needed.

Upgrade/switch the algorithm as follows:
 1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc).
 2. Select **Application Management** on the left sidebar and click **Application Info** on the row of the target application.
 3. Select the **Quick Start** tab and click **upgrade**, **asymmetric encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.

### 2. The demo is running on two mobile phones, but why can't they display the images of each other?
Please make sure that the two mobile phones use different `UserIDs` when running the demo, as TRTC does not support using the same `UserID` on two devices simultaneously; unless different `SDKAppIDs` are used.

### 3. What are the restrictions of the firewall?
As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) for assistance.
