This document describes how to quickly run the TRTC demo for Windows.

## Environment Requirements
### Developing for Windows using C++
- Microsoft Visual Studio (VS) 2015 or above (2015 is recommended) 
- TRTC SDK for Windows 8.0 or above (8.1 is recommended)

### Developing for Windows using C#
- VS 2015 or above (2017 is recommended)
- .Net Framework 4.0 or above (4.0 is recommended)

### Developing for Windows using Qt
- VS 2015 or above (2015 is recommended)
- Find the right version of Qt add-in for your VS on the official website, and download and install the [VSIX](https://download.qt.io/official_releases/vsaddin/) file.
- Open VS, in the menu bar, select `QT VS Tools > Qt Options > Qt Versions`, and add an MSVC compiler.
- Copy all the DLL files in `SDK/CPlusPlus/Win32/lib` to the `debug`/`release` folder of the project directory.
>! The `debug`/`release` folder is created automatically after environment setup is completed in VS.

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
[](id:step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Create Application** and enter the application name such as `TestTRTC`. If you have already created an application, click **Select Existing Application**.
3. Add or edit tags according to your actual business needs and click **Create**.
![](https://main.qcloudimg.com/raw/8dc52b5fa66ec4a5a4317719f9d442b9.png)
>?
>- An application name can contain up to 15 characters. Only digits, letters, Chinese characters, and underscores are allowed.
>- Tags are used to identify and organize your Tencent Cloud resources. For example, an enterprise may have multiple business units, each of which has one or more TRTC applications. In this case, the enterprise can tag TRTC applications to mark out the unit information. Tags are optional and can be added or edited according to your actual business needs.

[](id:step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code for your platform.
2. Click **Next**.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### Step 3. Configure demo project files
1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open the `GenerateTestUserSig` file:
 <table>
     <tr>
         <th nowrap="nowrap">Platform</th>  
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
  <ul><li>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.</li>
  <li>SECRETKEY: left empty by default. Set it to the actual key.</li></ul> 
  <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, please see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:step4)
### Step 4. Compile and run
- **Windows (C++):**
Use VS (VS 2015 is recommended) to open `DuilibDemo\TRTCDuilibDemo.sln` in the source code directory, and compile and run the demo project. We recommend building the project in the release mode for x86.
- **Windows (C#):**
Use VS (VS 2017 is recommended) to open `CSharpDemo\TRTCCSharpDemo.sln` in the source code directory, and compile and run the demo project. We recommend building the project in the release mode for x86.
- **Windows (QT):** 
Use VS (VS 2015 is recommended) to open
`QTDemo\QTDemo.pro` in the source code directory, and compile and run the QTDemo project.

## FAQs

### 1. Only public and private keys can be obtained when I try to view the key. How do I get a key?
TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** in the left navigation pane, find your application, and click **Application Info**.
 3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade.
  - Switch to the old algorithm ECDSA-SHA256:
      ![](https://main.qcloudimg.com/raw/96a974bcc25d0fab17db839be12fdb5e/%E8%B7%91%E9%80%9ADemo(Windows)2-%E8%BF%94%E8%BF%98.png)
  - Switch to the new algorithm HMAC-SHA256:
      ![](https://main.qcloudimg.com/raw/c3d53c405bb074ef4758cb12aa01e024/%E8%B7%91%E9%80%9ADemo(Windows)3-%E8%BF%94%E8%BF%98.png)

### 2. The demo is running on two devices, but why can't they display the images of each other?
Make sure that the two devices use different `UserIDs`. With TRTC, you cannot use the same `UserID` on two devices simultaneously unless the `SDKAppIDs` are different.


### 3. What are firewall restrictions does the SDK face?
The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, please see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).
