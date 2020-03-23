This document describes how to quickly run the Tencent Cloud TRTC Demo for iOS and macOS.

## Environment Requirements
- Xcode 9.0 or above
- Make sure that your project has a valid developer signature

## Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the [TRTC Console](https://console.cloud.tencent.com/rav) and click **Create Application**.
  If you already have an application, please note down its `SDKAppID` and then [download the SDK and demo source code](#step2) directly; otherwise, please proceed to the next step.
2. Enter the application's name and other information and click **OK**.
  After the application is created, an application ID (SDKAppID) will be automatically generated, which should be noted down.


<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Click the application card to enter the **Quick Start** page.
2. Click **iOS (V2)** or **macOS (V2)** in **Step 1: download SDK + auxiliary demo source code** to get redirected to [GitHub](https://github.com/tencentyun/TRTCSDK) (or visit [Gitee](https://gitee.com/cloudtencent/TRTCSDK)) and download the relevant SDK and demo source code.


<span id="step3"></span>
### Step 3. View and copy the encryption key
1. Click **View Key** in **Step 2: obtain the secret key to issue UserSig** to get the encryption key used to calculate `UserSig`.
2. Click **Copy Secret Key** to copy the key to the clipboard.


<h3 id="CopyKey">Step 4. Configure demo project files</h3>

 The `GenerateTestUserSig.h` file in the demo project can be used to calculate `UserSig` locally by using the HMAC-SHA256 algorithm for quick demo execution.

1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `GenerateTestUserSig.h` file.
  <table>
     <tr>
         <th nowrap="nowrap">Applicable Platform</th>
         <th nowrap="nowrap">Relative Path to File</th>
     </tr>
   <tr>
         <td>iOS</td>
   <td>iOS/TRTCDemo/TRTC/GenerateTestUserSig.h</td>
     </tr>
  <tr>
       <td>macOS</td>
       <td>Mac/TRTCDemo/TRTC/GenerateTestUserSig.h</td>
     </tr>
</table>
3. Set the relevant parameters in the `GenerateTestUserSig.h` file:
  - \_SDKAppID: please enter the actual `SDKAppID` obtained in [step 1](#step1).
  - \_SECRETKEY: please enter the actual key information obtained in [step 3](#step3).


>The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Server-side UserSig Generation](https://intl.cloud.tencent.com/document/product/647/35166#Server).

### Step 5. Compile and run
1. Enter the directory where the `TRTCSDK iOS/Mac Demo Podfile` file is located in a terminal window.
2. Run the `pod install` command to install the TRTC SDK, or run the `pod update` command to update the local library.
3. Use Xcode (v9.0 or above) to open the `TRTCDemo.xcworkspace` project in the source code directory, compile it, and run the demo project.

## FAQs

### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to click **Upgrade** in **Step 2: obtain the secret key to issue UserSig** to upgrade the signature algorithm before your can get a new encryption key. If you don't upgrade it, you can continue to use the [legacy algorithm](https://intl.cloud.tencent.com/document/product/647/35166#old-version-of-algorithm).

### 2. The demo is running on two mobile phone, but why can't they display the images of each other?
Please make sure that the two mobile phones use different `UserIDs` when running the demo, as TRTC does not support using the same `UserID` on two devices simultaneously; unless different `SDKAppIDs` are used.


### 3. What are the restrictions of the firewall?
As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please see [Dealing with Organizational Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) for assistance.
