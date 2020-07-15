This document describes how to quickly run the Tencent Cloud TRTC Demo for Electron.


## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name such as `TestTRTC`, and click **Create Application**.

<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding card, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)** to redirect to GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Electron_latest.zip)**) and download the relevant SDK and supporting demo source code.
 
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

<span id="step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `TRTCSDK/Electron/js/GenerateTestUserSig.js` file.
3. Set the relevant parameters in the `GenerateTestUserSig.js` file:
  <ul><li>SDKAPPID: it is 0 by default. Please replace it with your real `SDKAppID`.</li>
  <li>SECRETKEY: it is an empty string by default. Please replace it with your real key information.</li></ul> 
	<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png"/>
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage the application.

<span id="step4"></span>
### Step 4. Compile and run

#### Windows
1. Download the latest [Node.js](https://nodejs.org/en/download/) Windows Installer (.msi) 64-bit or Windows Installer (.msi) 32-bit based on your OS version.
2. Open the `Node.js command prompt` in the application list, start the command line window, point the directory to the target path extracted in [step 3](#step3), and run the following command:
```
npm install
```

3. If downloading the Electron compression package is slow, you can configure a mirror address or download the corresponding version and `SHASUMS256.txt` file from [GitHub](https://github.com/electron/electron/releases) to the `C:\Users\[your username]\AppData\Local\electron\Cache` directory.
4. After the npm dependent libraries are all installed, run the following command in the command line window to run the Electron demo.
```
npm start
```
![](https://main.qcloudimg.com/raw/1a69f78ecff302b4c7af7231ede5c9e1.png)


#### macOS
1. Open the Terminal window and run the following command to install Homebrew. Skip this step if you have already installed it.
```
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2. Run the following command to install Node.js.
```
$ brew install node
```
3. If installing Node.js with the default address of Homebrew is slow, you can consider using a mirror address.
```cmd
$ cd `brew --repo`
$ git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
$ brew update
```
4. Run the `cd` command to go to the target path extracted in [step 3](#step3) and run the following command.
```
npm install
```
![](https://main.qcloudimg.com/raw/a39debd89aa81d9eeb5ca34ccd32026b.png)
5. After the npm dependent libraries are all installed, run the following command in the command line window to run the Electron demo.
```
npm start
```
![](https://main.qcloudimg.com/raw/9e9558b0fd1aed0ba39594e4881b4394.png)


## FAQs

### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to upgrade the signature algorithm before your can get a new encryption key. If you don't upgrade it, you can continue to use the [legacy algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166).

Upgrade operation:
1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc).
2. Select **Application Management** on the left sidebar and click **Application Info** on the row of the target application.
3. Select the **Quick Start** tab and click **Upgrade** in **Step 2: obtain the secret key to issue UserSig**.

### 2. The demo is running on two devices, but why can't they display the images of each other?
Please make sure that the two devices use different `UserID` values when running the demo, as TRTC does not support using the same `UserID` on two devices simultaneously, unless different `SDKAppID` values are used.


### 3. What are the restrictions of the firewall?
As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) for assistance.
