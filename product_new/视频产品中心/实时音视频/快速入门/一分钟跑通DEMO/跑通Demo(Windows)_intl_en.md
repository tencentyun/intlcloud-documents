This document describes how to quickly run the Tencent Cloud TRTC Demo for Windows.

## Environment Requirements
**Windows (C++) development environment**
- Microsoft Visual Studio 2015 or above (v2015 is recommended) 
- Windows SDK 8.0 or above (v8.1 is recommended)

**Windows (C#) development environment**
- Microsoft Visual Studio 2015 or above (v2017 is recommended)
- .Net Framework 4.0 or above (v4.0 is recommended)

## Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the [TRTC Console](https://console.cloud.tencent.com/rav) and click **Create Application**.
 If you already have an application, please note down its `SDKAppID` and then [download the SDK and demo source code](#step2) directly; otherwise, please proceed to the next step.
2. Enter the application's name and other information and click **OK**.
 After the application is created, an application ID (SDKAppID) will be automatically generated, which should be noted down.
 ![](https://main.qcloudimg.com/raw/1acc030cfc47e32bc36873c9a494b88a.png)

<span id="step2"></span>
### Step 2. Download and decompress the SDK and demo source code
>?If your network is very slow to access GitHub, you are recommended to download the SDK and auxiliary demo source code through **method 1**.

**Method 1**
Download the [SDK and demo source code for Windows](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip).


**Method 2**
1. Click the application card to enter the **Quick Start** page.
2. Click **Windows(V2)** in **Step 1: download SDK + auxiliary demo source code** to get redirected to [GitHub](https://github.com/tencentyun/TRTCSDK) (or visit [Gitee](https://gitee.com/cloudtencent/TRTCSDK)) and download and decompress the relevant demo source code.
 ![](https://main.qcloudimg.com/raw/1bc8fdb853ab6b8bdf5b398c6efa1623.png)
3. Download and decompress the [SDK](https://github.com/tencentyun/TRTCSDK/tree/master/Windows/SDK) source code.
4. Copy and replace all files in the `SDK` directory obtained by decompressing the SDK source code into the `Windows/SDK` directory of the demo source code.

<span id="step3"></span>
### Step 3. View and copy the encryption key
1. Click **View Key** in **Step 2: obtain the secret key to issue UserSig** to get the encryption key used to calculate `UserSig`.
2. Click **Copy Secret Key** to copy the key to the clipboard.
 ![](https://main.qcloudimg.com/raw/d0b780f7b28833533e12807d1b11d8be.png)

<h3 id="CopyKey">Step 4. Configure demo project files</h3>
 The `GenerateTestUserSig` file in the demo project can be used to calculate `UserSig` locally by using the HMAC-SHA256 algorithm for quick demo execution.

1. In the directory of demo source package extracted in [step 2](#step2), locate and open the `GenerateTestUserSig` file.
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
2. Set the relevant parameters in the `GenerateTestUserSig` file. Windows (C++) is used as an example in the figure below for your reference:
  - SDKAppID: please enter the actual `SDKAppID` obtained in [step 1](#step1).
  - SECRETKEY: please enter the actual key information obtained in [step 3](#step3).
    ![](https://main.qcloudimg.com/raw/c8dd14631e8f976944376ba58e9c1079.png)

>!The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Server-side UserSig Generation](https://intl.cloud.tencent.com/document/product/647/35166#Server).

### Step 5. Compile and run
- **Windows (C++)**
Use Visual Studio (VS 2015 is recommended) to open the `DuilibDemo\TRTCDuilibDemo.sln` project file in the source code directory. You are recommended to select the Release/X86 platform to compile and run the demo project.

- **Windows (C#)**
Use Visual Studio (VS 2017 is recommended) to open the `CSharpDemo\TRTCCSharpDemo.sln` project file in the source code directory. You are recommended to select the Release/X86 platform to compile and run the demo project.

## FAQs

### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to click **Upgrade** in **Step 2: obtain the secret key to issue UserSig** to upgrade the signature algorithm before your can get a new encryption key. If you don't upgrade it, you can continue to use the [legacy algorithm](https://intl.cloud.tencent.com/document/product/647/35166#.E8.80.81.E7.89.88.E6.9C.AC.E7.AE.97.E6.B3.95) ECDSA-SHA256.

### 2. The demo is running on two mobile phone, but why can't they display the images of each other?
Please make sure that the two mobile phones use different `UserIDs` when running the demo, as TRTC does not support using the same `UserID` on two devices simultaneously; unless different `SDKAppIDs` are used.
![](https://main.qcloudimg.com/raw/c7b1589e1a637cf502c6728f3c3c4f99.png)

### 3. What are the restrictions of the firewall?
As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please see [Dealing with Organizational Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35123/35164) for assistance.
