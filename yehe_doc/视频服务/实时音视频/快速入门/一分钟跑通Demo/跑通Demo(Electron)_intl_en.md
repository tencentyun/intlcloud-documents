This document describes how to quickly run the Tencent Cloud TRTC Demo for Electron.

## Prerequisites

You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions

<span id="step1" name="step1"> </span>

### Step 1. Create an application

1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name such as `TestTRTC`, and click **Create Application**.

<span id="step2" name="step2"> </span>

### Step 2. Download the SDK and demo source code

1. Mouse over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)** to enter GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Electron_latest.zip)**), and download the relevant SDK and supporting demo source code.
    ![img](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

<span id="step3" name="step3"> </span>

### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#step2) and find the `TRTCSDK/Electron/TRTCSimpleDemo/` directory, which is the <span id="projectFolder" name="projectFolder">"**project directory**"</span> mentioned below.

2. Find the `debug/gen-test-user-sig.js` file in the project directory and open it.

3. Set the relevant parameters in the `gen-test-user-sig.js` file:

    -   SDKAPPID: it is 0 by default. Please replace it with your real `SDKAppID`.
    -   SECRETKEY: it is an empty string by default. Please replace it with your real key information.
    
4. Return to the TRTC Console and click **Pasted and Next**.

5. Click **Close Guide and Enter Console** to manage the application.

**File and directory description:**

```bash
.
|---README.md                             README file. Please read it carefully
|---main.electron.js                      Electron main file
|---public                                Stores static files
|---babel.config.js
|---package.json
|---vue.config.js                         vue-cli project file
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
| | |---log.js														Log tool
| | |---mtah5.js													
| | |---routes.js
| | |---rand.js
| |---pages                               Page directory
| | |---index.vue                         Homepage
| | |---trtc                              Video conferencing pages
| | | |---trtc-room.vue                   Video conferencing room page
| | | |---trtc-index.vue                  Video conferencing entry page
| | |---404.vue
| | |---live                              Live streaming pages
| | | |---live-index.vue                  Live streaming entry page
| | | |---live-room-audience.vue          Viewer page
| | | |---live-room-anchor.vue            Anchor page
| |---debug                               Note: when deploying, please move the signature logic in this folder to the server for implementation
| | |---lib-generate-test-usersig.min.js  
| | |---gen-test-user-sig.js              
```

<span id="step4"> </span>

### Step 4. Compile and run

#### Windows

1. Install the latest version of Node.js. We recommend you choose a 64-bit `.msi` file. [Node.js download address](https://nodejs.org/en/download/)

2. Press the `win + r` and enter `cmd` to open the command line window as administrator, locate the [project directory](#projectFolder), and run the following command.
	
```shell
$ npm install
```
	
![](https://main.qcloudimg.com/raw/5aba25ba2d5eddb5d956406ca5b6b9ac.png)


3. After the npm dependent libraries are all installed, run the following command in the command line window to run the demo.

    ```shell
    $ npm run start  # During the first run, the UI will appear in the window after a while
    ```
    
    ![](https://main.qcloudimg.com/raw/47f6e01acb2d927f6d9e24a7c9f78af1.png)

#### macOS

1. Open the Terminal or command line window and run the following command to install Homebrew. Skip this step if you have already installed it.

    ```shell
    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    ```

2. Run the following command to install Node.js.

    ```shell
    $ brew install node
    ```

3. If installing Node.js with the default address of Homebrew is slow, you can consider using a mirror address.

    ```shell
    $ cd `brew --repo`
    $ git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
    $ brew update
    ```

4. Run the `cd` command to go to the project directory and run the following command.

    ```shell
    $ npm install 
    ```
    
    ![](https://main.qcloudimg.com/raw/3f8e92e9c59ff1bdb9fd0b2a0f34852a.png)
    
5. After the npm dependent libraries are all installed, run the following command in the command line window to run the demo.

    ```shell
    $ npm run start # During the first run, the UI will appear in the window after a while
    ```
    
	![](https://main.qcloudimg.com/raw/423dae368118e5250e7fa878022bb26f.png)
    
### Main project commands

| Command | Description |
|--|--|
| npm run start | Runs the demo in the development environment |
| npm run pack:mac | Packages as a .dmg installation file for macOS |
| npm run pack:win64 | Packages as an .exe installation file for Windows 64-bit |

## FAQs

### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?

Starting from TRTC SDK 6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to upgrade the signature algorithm before your can get a new encryption key. If you don't upgrade it, you can continue to use the [legacy algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166).

**Upgrade operation:**

1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc).
2. Select **Application Management** on the left sidebar and click **Application Info** on the row of the target application.
3. Select the **Quick Start** tab and click **Upgrade** in **Step 2: obtain the secret key to issue UserSig**.

### 2. The demo is running on two devices, but why can't they display the images of each other?

Please make sure that the two devices use different `UserID` values when running the demo, as TRTC does not support using the same `UserID` on two devices simultaneously, unless different `SDKAppID` values are used.

### 3. What are the restrictions of the firewall?

As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) for assistance.


