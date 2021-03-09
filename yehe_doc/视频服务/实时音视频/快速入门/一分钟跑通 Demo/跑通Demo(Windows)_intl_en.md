This document describes how to quickly run the Tencent Cloud TRTC demo for Windows.

## Environment Requirements
**Windows (C++) development environment**
- Microsoft Visual Studio 2015 or above (VS 2015 is recommended) 
- Windows SDK 8.0 or above (8.1 is recommended)

**Windows (C#) development environment**
- Microsoft Visual Studio 2015 or above (VS 2017 is recommended)
- .Net Framework 4.0 or above (4.0 is recommended)

**Windows (C#) development environment**
- Microsoft Visual Studio 2015 or above (VS 2015 is recommended)





## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Operation Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name such as `TestTRTC`, and click **Create Application**.

<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Windows)** to visit GitHub (or click **[ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip?_ga=1.195966252.185644906.1567570704)**), and download the SDK and demo source code.
 ![](https://main.qcloudimg.com/raw/73b9bfa89b42acbc166074a29f20be47.png)
2. After the download, return to the TRTC console and click **Downloaded and Next** to view your `SDKAppID` and secret key.

<span id="step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `GenerateTestUserSig` file:
 <table>
     <tr>
         <th nowrap="nowrap">Applicable Platform</th>  
         <th nowrap="nowrap">Relative Path to File</th>  
     </tr>
   <tr>      
         <td>Windows (C++)</td>   
       <td>Windows/DuilibDemo/GenerateTestUserSig.h</td>   
     </tr> 
   <tr>
       <td>Windows (C#)</td>   
       <td>Windows/CSharpDemo/GenerateTestUserSig.cs</td>
     </tr> 
 </table>
3. Set parameters in the `GenerateTestUserSig.js` file:
  <ul><li>SDKAPPID: 0 by default. Set it to the actual SDKAppID.</li>
  <li>SECRETKEY: left empty by default. Set it to the actual secret key.</li></ul> 
  <img src="https://main.qcloudimg.com/raw/6a95980aa101276c8bf8340cf0a5d99f/%E8%B7%91%E9%80%9ADemo(Windows)0-%E8%BF%94%E8%BF%98.png">
4. Return to the TRTC console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console to Manage Applications**.

>!The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

<span id="step4"></span>
### Step 4. Compile and run the project.
- **Windows (C++)**
Use Visual Studio (VS 2015 is recommended) to open the `DuilibDemo\TRTCDuilibDemo.sln` project file in the source code directory. Consider using the Release/x86 platform to compile and run the demo project.
- **Windows (C#)**
Use Visual Studio (VS 2017 is recommended) to open the `CSharpDemo\TRTCCSharpDemo.sln` project file in the source code directory. Consider using the Release/x86 platform to compile and run the demo project.
 



## FAQ

### 1. Only public and private key information can be obtained when I try to view the secret key. How do I get the secret key?
TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new secret key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** on the left sidebar, find the target application, and click **Application Info**.
 3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade:
  - Switch to the old algorithm ECDSA-SHA256:
      ![](https://main.qcloudimg.com/raw/96a974bcc25d0fab17db839be12fdb5e/%E8%B7%91%E9%80%9ADemo(Windows)2-%E8%BF%94%E8%BF%98.png)
  - Switch to the new algorithm HMAC-SHA256.
      ![](https://main.qcloudimg.com/raw/c3d53c405bb074ef4758cb12aa01e024/%E8%B7%91%E9%80%9ADemo(Windows)3-%E8%BF%94%E8%BF%98.png)

### 2. The demo is running on two devices, but why can't they display the images of each other?
Make sure that the two devices use different `UserIDs`. With TRTC, you cannot use the same `UserID` on two devices simultaneously unless the `SDKAppIDs` are different.

### 3. What firewall restrictions does the SDK face?
The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) for assistance.
