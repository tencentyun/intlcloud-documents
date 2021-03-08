This document describes how to quickly run the TRTC demo for iOS and macOS.

## Environment Requirements
- Xcode 11.0 or above
- Your project has a valid developer signature.
- Qt Creator 4.13.3 (macOS) or above

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
[](id:step1)
### Step 1. Create an application.
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g. `TestTRTC`, and click **Create**.

[](id:step2)
### Step 2. Download the SDK and demo source code.
1. Download the SDK and demo source code for your platform.
2. Click **Next step**.

[](id:step3)
### Step 3. Configure demo project files.
1. In the **Modify Configuration** step, select the platform in line with the source package downloaded.
2. Find and open the `GenerateTestUserSig.h` file.
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
    <td>Mac/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h</td>
  </tr></table>
3. Set parameters in `GenerateTestUserSig.h` as follows.
  <ul><li>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.</li>
  <li>SECRETKEY: left empty by default. Set it to the actual key.</li></ul> 
4. Click **Next step** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Compile and run the project.
1. In a terminal window, go to the `TRTCScenesDemo > Podfile` directory of the source code.
2. Run `pod install` to install the TRTC SDK, or run `pod update` to update the local library.
3. Use Xcode (11.0 or above) to open `TXLiteAVDemo.xcworkspace` in the source code directory, and compile and run the project.
>? If you use Qt Creator (4.13.3 or above), open `QTDemo.pro` in the source code directory, and compile and run the demo project.

## FAQs
### 1. Only public and private keys can be obtained when I try to view the key. How do I get a key?
TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** in the left navigation pane, find your application, and click **Application Info**.
 3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade:
  - Switch to the old algorithm ECDSA-SHA256:
      ![](https://main.qcloudimg.com/raw/bc5cc756b93bd3e688f9f31a9c1efdfe/%E8%B7%91%E9%80%9ADemo(iOS&Mac)5-%E8%BF%94%E8%BF%98.png)
  - Switch to the new algorithm HMAC-SHA256.
      ![](https://main.qcloudimg.com/raw/2f55ac47bbff3257bfadc7e670e0ff1c/%E8%B7%91%E9%80%9ADemo(iOS&Mac)6-%E8%BF%94%E8%BF%98.png)

### 2. The demo is running on two mobile phones, but why can't they display the images of each other?
Make sure that the two mobile phones use different `UserIDs`. With TRTC, you cannot use the same `UserID` on two devices simultaneously unless the `SDKAppIDs` are different.

### 3. What firewall restrictions does the SDK face?
The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).
