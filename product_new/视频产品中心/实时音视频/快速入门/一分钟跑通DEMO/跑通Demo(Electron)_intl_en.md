This document describes how to quickly run the Tencent Cloud TRTC Demo for Electron.

## Environment Requirements

#### Windows 

Go to the [download address](https://nodejs.org/en/download/), select the Windows 32-bit version, and install the node environment.

>!The TRTC SDK for Electron currently only supports the Windows 32-bit version.

### macOS

Install node by running the following command:
```
brew install node
```

## Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the [TRTC Console](https://console.cloud.tencent.com/rav) and click **Create Application**.
 If you already have an application, please note down its `SDKAppID` and then [download the SDK and demo source code](#step2) directly; otherwise, please proceed to the next step.
2. Enter the application's name and other information and click **OK**.
 After the application is created, an application ID (SDKAppID) will be automatically generated, which should be noted down.
![](https://main.qcloudimg.com/raw/1acc030cfc47e32bc36873c9a494b88a.png)

<span id="step2"></span>
### Step 2. Download the demo source code
[Download](https://gitee.com/vqcloud/Trtc_Electron_Demo.git) the demo source code.

<span id="step3"></span>
### Step 3. View and copy the encryption key
1. Click **View Key** in **Step 2: obtain the secret key to issue UserSig** to get the encryption key used to calculate `UserSig`.
2. Click **Copy Secret Key** to copy the key to the clipboard.
 ![](https://main.qcloudimg.com/raw/d0b780f7b28833533e12807d1b11d8be.png)
 
<span id="step4"></span>
### Step 4. Configure demo project files
The `GenerateTestUserSig.js` file in the demo project can be used to calculate `UserSig` locally by using the HMAC-SHA256 algorithm for quick demo execution.

1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `TRTC_Electron_Demo/js/GenerateTestUserSig.js` file.
3. Set the relevant parameters in the `GenerateTestUserSig.h` file:
  - SDKAPPID: please enter the actual `SDKAppID` obtained in [step 1](#step1).
  - PRIVATEKEY: please enter the actual key information obtained in [step 3](#step3).
  ![](https://main.qcloudimg.com/raw/9275a5f99bf00467eac6c34f6ddd3ca5.jpg)

<span id="step5"></span>
### Step 5. Compile and run

Run the following command in the `TRTC_Electron_Demo` directory:
```js
npm install  // Download the npm package
npm start    // Start running
```

## FAQs

### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to click **Upgrade** in **Step 2: obtain the secret key to issue UserSig** to upgrade the signature algorithm before your can get a new encryption key. If you don't upgrade it, you can continue to use the [legacy algorithm](https://intl.cloud.tencent.com/document/product/647/35166#.E8.80.81.E7.89.88.E6.9C.AC.E7.AE.97.E6.B3.95) ECDSA-SHA256.

### 2. The demo is running on two mobile phone, but why can't they display the images of each other?
Please make sure that the two mobile phones use different `UserIDs` when running the demo, as TRTC does not support using the same `UserID` on two devices simultaneously; unless different `SDKAppIDs` are used.
![](https://main.qcloudimg.com/raw/c7b1589e1a637cf502c6728f3c3c4f99.png)

### 3. What are the restrictions of the firewall?
As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please see [Dealing with Organizational Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) for assistance.
