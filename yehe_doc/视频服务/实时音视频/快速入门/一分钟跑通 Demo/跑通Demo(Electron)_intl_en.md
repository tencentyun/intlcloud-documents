This document describes how to quickly run the TRTC demo for Electron.

## Prerequisites

You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions

[](id:step1)

### Step 1. Create an application
1. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestTRTC` and click **Create**. If you have already created an application, click **Existing** to select it.
3. Add or edit tags for your application if necessary, and click **Create**.
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
2. Find and open the `Electron/js/GenerateTestUserSig.js` file.
3. Set parameters in the `GenerateTestUserSig.js` file:
<ul>
 <li/>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.
 <li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
 <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

**File paths and description:**
```bash
.
|---README.md                             README file. Please read it carefully.
|---main.electron.js                      Main Electron file
|---public                                Static files
|---babel.config.js
|---package.json
|---vue.config.js                         Vue CLI project file
|---src                                   Source code directory
| |---app.vue
| |---common.css
| |---main.js
| |---components                          UI component
| | |---main-menu.vue
| | |---nav-bar.vue
| | |---show-screen-capture.vue
| |---common                              Utility functions, public libraries, etc.
| | |---live-room-service.js
| | |---log.js                            Log tools
| | |---mtah5.js                          
| | |---routes.js
| | |---rand.js
| |---pages                               Views
| | |---index.vue                         Homepage
| | |---trtc                              Video conferencing views
| | | |---trtc-room.vue                   Video conferencing room view
| | | |---trtc-index.vue                  Video conferencing entry view
| | |---404.vue
| | |---live                              Live streaming views
| | | |---live-index.vue                  Live streaming entry view
| | | |---live-room-audience.vue          Audience room view
| | | |---live-room-anchor.vue            Anchor room view
| |---debug                               When deploying your project, please move the signature logic in this folder to the server for implementation.
| | |---lib-generate-test-usersig.min.js  
| | |---gen-test-user-sig.js              
```

[](id:step4)

### Step 4. Compile and run
<dx-tabs>
::: Windows
1. Install the latest version of Node.js. We recommend you use a 64-bit MSI file for the installation. Download [here](https://nodejs.org/en/download/).
2. Press Windows+R and type `cmd` to open the Command Prompt as an administrator, locate the [project directory](#projectFolder), and run the following command.
```shell
$ npm install
​```![Installing](https://main.qcloudimg.com/raw/5aba25ba2d5eddb5d956406ca5b6b9ac.png)

4. After the npm dependencies are installed, run the following command in the Command Prompt to run the demo.
​```shell
$ npm run start  # On first run, it may take a while to show the UI.
​```![Running the demo](https://main.qcloudimg.com/raw/47f6e01acb2d927f6d9e24a7c9f78af1.png)

:::
::: macOS
1. Open a terminal window or Command Prompt and run the following command to install Homebrew. If you have already installed it, skip this step.
​```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2. Run the following command to install Node.js.
```shell
$ brew install node
```

3. If it is too slow for you to install Node.js via Homebrew, consider using a mirror address in your country or region.
 ```shell
$ cd `brew --repo`
$ git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
$ brew update
 ```

4. Run the `cd` command to go to the project directory and run the following command.
```shell
$ npm install 
​```![](https://main.qcloudimg.com/raw/8bcc95adad07ff37e7f0a27893b8b7cf.png)

5. After the npm dependencies are installed, run the following command in the Command Prompt to run the demo.
​```shell
$ npm run start # On first run, it may take a while to show the UI.
​```![Running the project in macOS](https://main.qcloudimg.com/raw/423dae368118e5250e7fa878022bb26f.png)
:::
</dx-tabs>
    
### Main project commands

| Command | Description |
|--|--|
| npm run start | Runs the demo in development environment. |
| npm run pack:mac | Packages the project into a DMG installer for macOS. |
| npm run pack:win64 | Packages the project into a 64-bit EXE installer for Windows. |

## FAQs

### 1. Only public and private keys can be obtained when I try to view the key. How do I get a key?

TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166).

**Upgrade:**
1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
2. Click **Application Management** on the left sidebar, find your application, and click **Application Info**.
3. Select the **Quick Start** tab and click **upgrade** in **Step 2: obtain the secret key to issue UserSig**.

### 2. The demo is running on two devices, but why can't they display the images of each other?

Make sure that the two devices use different `UserIDs`. With TRTC, you cannot use the same `UserID` on two devices simultaneously unless the `SDKAppIDs` are different.

![](https://main.qcloudimg.com/raw/9a03335e435de0f12e2a26882f53db02.png)

### 3. What firewall restrictions does the SDK face?

The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).

>? For more FAQs, see [Electron](https://intl.cloud.tencent.com/document/product/647/43093).

## Technical Support
[Contact us](https://intl.cloud.tencent.com/contact-us) if you have any questions.


## References

- [SDK API Guide](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- [SDK Update Log](https://intl.cloud.tencent.com/document/product/647/38702)
- [Simple Demo Source Code](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTCSimpleDemo)
- [API Example Source Code](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTC-API-Example)
- [FAQs](https://intl.cloud.tencent.com/document/product/647/43093)

```