This document describes how to quickly run the TRTC demo for Electron.

## Prerequisites

You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions

[](id:step1)

### Step 1. Create an application

1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g., `TestTRTC`, and click **Create**.

[](id:step2)

### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code for your platform.
2. Click **Next**.

[](id:step3)
### Step 3. Configure demo project files
1. In the **Modify Configuration** step, select the platform in line with the source package downloaded.
2. Decompress the source package and find the `TRTCSDK/Electron/TRTCSimpleDemo/` directory, which is the <span id="projectFolder"></span>"**project directory**" mentioned below.
2. Find and open the `debug/gen-test-user-sig.js` file in the project directory.
3. Set parameters in `gen-test-user-sig.js` as follows:
<ul>
 <li/>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
 <li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

**File paths and description:**
```bash
.
|---README.md                             README file. Please read it carefully.
|---main.electron.js                      Electron main file
|---public                                Stores static files
|---babel.config.js
|---package.json
|---vue.config.js                         Vue CLI project file
|---src                                   Source code directory
| |---app.vue
| |---common.css
| |---main.js
| |---components                          UI component directory
| | |---main-menu.vue
| | |---nav-bar.vue
| | |---show-screen-capture.vue
| |---common                              Utility functions, public libraries, etc.
| | |---live-room-service.js
| | |---log.js                            Log tools
| | |---mtah5.js                          
| | |---routes.js
| | |---rand.js
| |---pages                               View directory
| | |---index.vue                         Homepage
| | |---trtc                              Video conferencing views
| | | |---trtc-room.vue                   Video conferencing room view
| | | |---trtc-index.vue                  Video conferencing entry view
| | |---404.vue
| | |---live                              Live streaming views
| | | |---live-index.vue                  Live streaming entry view
| | | |---live-room-audience.vue          Viewer room view
| | | |---live-room-anchor.vue            Anchor room view
| |---debug                               Note: when deploying your project, please move the signature logic in this folder to the server for implementation.
| | |---lib-generate-test-usersig.min.js  
| | |---gen-test-user-sig.js              
```

[](id:step4)

### Step 4. Compile and run the demo
#### Windows
1. Install the latest version of Node.js. We recommend you use a 64-bit MSI file for the installation. Download [here](https://nodejs.org/en/download/).
2. Press the Windows key and R and enter `cmd` to open Windows Command Prompt as Administrator, locate the [project directory](#projectFolder), and run the following command.
```shell
$ npm install
```
![](https://main.qcloudimg.com/raw/5aba25ba2d5eddb5d956406ca5b6b9ac.png)
3. After the npm dependencies are installed, run the following command in Command Prompt to run the demo.
```shell
$ npm run start  # During the first run, the UI will appear in the window after a while
```
![](https://main.qcloudimg.com/raw/47f6e01acb2d927f6d9e24a7c9f78af1.png)



#### macOS
1. Open a terminal window or Command Prompt and run the following command to install Homebrew. If you have already installed it, skip this step.
```shell
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
```

5. After the npm dependencies are installed, run the following command in Command Prompt to run the demo.
```shell
$ npm run start # On first run, it may take a while for the UI to appear.
```

### Main project commands

| Command | Description |
|--|--|
| npm run start | Runs the demo in development environment. |
| npm run pack:mac | Packages the project into a DMG installer for macOS |
| npm run pack:win64 | Packages the project into a 64-bit EXE installer for Windows |

## FAQs

### 1. Only public and private keys can be obtained when I try to view the key. How do I get a key?

TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166).

**Upgrade:**
1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
2. Click **Application Management** in the left navigation pane, find your application, and click **Application Info**.
3. Select the **Quick Start** tab and click **Upgrade** in **Step 2: obtain the secret key to issue UserSig**.

### 2. The demo is running on two devices, but why can't they display the images of each other?

Make sure that the two devices use different `UserIDs`. With TRTC, you cannot use the same `UserID` on two devices simultaneously unless the `SDKAppIDs` are different.

### 3. What are firewall restrictions does the SDK face?

The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, please see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).
