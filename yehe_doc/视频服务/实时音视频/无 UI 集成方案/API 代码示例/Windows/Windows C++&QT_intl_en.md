This document describes how to quickly run the demo for the TRTC Windows C++/Qt SDK.

## Environment Requirements
- Install Visual Studio 2017 or later (v2019 is recommended).
- Install [Qt 5.14.x](https://download.qt.io/archive/qt/5.14/5.14.2/).
- Find the right version of Qt Add-in for your Visual Studio on the [Qt website](https://download.qt.io/official_releases/vsaddin/2.7.2/). Download and install it.
- Open Visual Studio, in the menu bar, select **QT VS Tools > Qt Options > Qt Versions**, and add a MSVC compiler.
- Copy all the DLL files in `SDK/CPlusPlus/Win64/lib` (for 64-bit Windows) to the `debug`/`release` folder of the project directory.
>! `debug/release` is auto-generated after environment configuration in Visual Studio. For 32-bit Windows, copy all the DLL files in `SDK/CPlusPlus/Win64/lib` to the `debug/release` folder of the project directory.


## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
[](id:step1)
### Step 1. Create an application
1. In the TRTC console, click **Development Assistance** > [Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart).
2. Select **New** and enter an application name such as `TestTRTC`. If you have already created an application, select **Existing**.
3. Add or edit tags according to your needs and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/7d1d1940f02ee954c369b5f749e0c663.png)
>?
>- An application name can contain up to 15 characters. Only digits, letters, Chinese characters, and underscores are allowed.
>- Tags are used to identify and organize your Tencent Cloud resources. For example, an enterprise may have multiple business units, each of which has one or more TRTC applications. In this case, the enterprise can tag TRTC applications to mark out the unit information. Tags are optional and can be added or edited according to your actual business needs.

[](id:step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code.
2. Click **Next**.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### Step 3. Configure the demo project file
1. In the **Modify Configuration** step, select your platform.
2. Find and open the file in which `SDKAppID` and secret key are defined.
 <table>
     <tr>
         <th nowrap="nowrap">Platform</th>  
         <th nowrap="nowrap">Relative Path to File</th>  
     </tr>
     <tr>      
         <td>Windows(C++/QT)</td>   
         <td>Windows/QTDemo/src/Util/defs.h</td>   
     </tr>
 </table>
3. Set the parameters in `defs.h` as follows:
  <ul><li>SDKAppID: `0` by default. Set it to the actual `SDKAppID`.</li>
  <li>SECRETKEY: Left empty by default. Set it to the actual key.</li></ul>
  <img src="https://qcloudimg.tencent-cloud.cn/raw/e210b7b71cf273de59d6e2df917101e4.png">
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- In this document, the method to obtain `UserSig` is to configure the secret key in the client code. In this method, the secret key is vulnerable to decompilation and reverse engineering. Once your secret key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and debugging**.
>- The best practice is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [How do I calculate `UserSig` during production?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:step4)
### Step 4. Compile and run the demo
- **Method 1:** Open the `QTDemo\QTDemo.pro` file in the source code directory with Qt Creator. Compile and run the `QTDemo` project.
- **Method 2:** Open Visual Studio (preferably v2015 or later and with the Qt Add-in installed). In the menu bar, select **Qt VS Tools** > **Open Qt Project File(.pro)...**, and open the `QTDemo\QTDemo.pro` file in the source code directory. Compile and run the `QTDemo` project.

## FAQs

### 1. There is only information of the public and private keys when I try to view the secret key. How do I get the secret key?
TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** on the left sidebar, find your application, and click **Application Info**.
 3. Select the **Quick Start** tab and click **Upgrade**, **asymmetric encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade
  - Switch to the old algorithm ECDSA-SHA256:
      ![](https://main.qcloudimg.com/raw/49da46eea23847de79925a12e7a07102/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)4-%E8%BF%94%E8%BF%98.png)
  - Switch to the new algorithm HMAC-SHA256:
      ![](https://main.qcloudimg.com/raw/fbb69de98ae6ec0c6e1d09c8d95d57b7/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)5-%E8%BF%94%E8%BF%98.png)

### 2. The demo is running on two devices, but why can't they display the images of each other?
Make sure that the two devices use different `UserID`. With TRTC, you cannot use the same `UserID` on two devices simultaneously unless the `SDKAppID` is different.

### 3. What firewall restrictions does the SDK face?
The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).
