## Free Demo
<input type="button" value="Windows" style="height: 30px;width: 150px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;margin-right:10px;"  onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-windows-latest.zip')" />

<input type="button" value="macOS" style="height: 30px;width: 150px;margin-top: 5px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-mac-latest.zip')" />

## Demonstration
You can install our demo app to experiment with our real-time interactive teaching solution. It offers not only basic capabilities such as audio/video call, screen sharing, whiteboard, and chat, but also advanced features such as mute all, raise hand to speak, invite users to speak, roll call, and sign-in.



## Using the Source Code for Real-Time Interactive Teaching
[](id:step1)
### Step 1. Create an application and get the SDKAppID and key
If you already have a TRTC application, you can skip this step and use your application’s SDKAppID and key.

1. Log in to the TRTC console, click **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**, enter your application name, such as `TestTRTC`, and click **Create**.  

2. Click **Next**. In the **Modify Configuration** step, note the SDKAppID and key.


[](id:step2)
### Step 2. Configure the IM application
>?The real-time interactive teaching solution is based on two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. For its billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

1. Click **Relevant Cloud Services** in the left sidebar and then click **IM Console > Application List**.

2. Click the application you created.

3. Click **Feature Configuration** > **Login and Message**. Under **Login Settings**, click **Edit**, and set the **Max Login Instances per User per Platform** for web to 2 or larger (the demo app requires login to only 2 IM instances, but you can set this value higher in case you need more in the future).


[](id:step3)
### Step 3. Set up the environment
Node.js and Yarn are required for the source code to run.

1. **Install Node.js:**
Install [Node.js](https://nodejs.org/en/download/) (preferably a version higher than 14.16.0). Run the terminal command below to check the version.
```
node --version
```
2. **Install Yarn:**
 - If the Node.js version is lower than 14.16.0, run the terminal command below to install [Yarn](https://yarnpkg.com/getting-started/install).
```
npm i -g corepack
```
 - If the Node.js version is higher than 14.16.0, run the terminal command below to install Yarn.
```
corepack enable
```
>! On Windows 10 or 11, if an error occurs because of insufficient permissions, try running the commands as administrator in the Command Prompt.



[](id:step4)
### Step 4. Clone the code

[Download a ZIP file of the code](https://github.com/TencentCloud/trtc-education-electron). After decompressing the file, you can find the code in `trtc-education-electron`. If you use [git](https://git-scm.com/downloads) to clone the code, run the following terminal command:

```
git clone https://github.com/TencentCloud/trtc-education-electron.git

cd trtc-education-electron
```

[](id:step5)
### Step 5. Obtain the `SDKAppID` and key
1. Find and open `src/main/config/generateUserSig.js`.
2. Set the parameters required to generate UserSig:
   - SDKAPPID: `0` by default. Set it to the `SDKAppID` obtained in [Step 1](#step1).
   - SECRETKEY: an empty string by default. Set it to the key obtained in [Step 1](#step1).

>!
>- In this document, the method to obtain UserSig is to configure a SECRETKEY in the client code. In this method, the SECRETKEY is vulnerable to decompilation and reverse engineering. Once your SECRETKEY is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and feature debugging**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:step6)
### Step 6. Run the code
Open `trtc-education-electron` in a terminal and run the following command:
```
yarn

yarn start
```
>!
>- On Windows 10 or 11, when you run the Yarn command for the first time to install dependencies, if an error occurs because of insufficient permissions, run the command as administrator in the Command Prompt first. After that, you can run the command as an ordinary user in the Command Prompt or a terminal of your code editor such as Visual Studio Code or WebStorm.
>- If your download of the Electron code is slow or stuck, you can [contact us](https://intl.cloud.tencent.com/contact-us) for help.

[](id:step7)
### Step 7. Create an installer and run it
Open `trtc-education-electron` in a terminal and run the command below to create an installer. After it is created, find the installer in `trtc-education-electron/build/release`, and then run it.

```
yarn package
```

>! You need macOS to create a macOS installer and Windows to create a Windows installer.


## Technical Support
If you have other questions, you can [fill out a contact form](https://intl.cloud.tencent.com/contact-us) or email colleenyu@tencent.com.

## Learn More

- [SDK API Guide](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- [Release Notes (Electron)](https://intl.cloud.tencent.com/document/product/647/38702)
- [Simple Demo Source Code](https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTCSimpleDemo)
- [API Example Source Code](https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTC-API-Example)
- [FAQs](https://intl.cloud.tencent.com/document/product/647/43093)
