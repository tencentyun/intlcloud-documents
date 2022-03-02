This document describes how to quickly run the IM demo for Electron.

## Environment Requirements

| Platform | Version |
|---------|---------|
| Electron | 13.1.5 or higher |
| Node.js | v14.2.0 |

## Prerequisites

You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
[](id:step1)
## Step 1. Create an App
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
>? If you already have an app, record its SDKAppID and [obtain key information](#step2).
>A Tencent Cloud account can create a maximum of 300 IM apps. If you want to create more apps, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first and then create a new one. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost. Proceed with caution**.
>
2. Click **Create Application**, enter your app name, and click **Confirm**.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. After creation, you can see the status, service version, SDKAppID, creation time, and expiry time of the new app on the overview page of the console. Record the SDKAppID.
    ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. Click the created app. In the left sidebar, click **Auxiliary Tools** -> **UserSig Tools** to create a UserID and the corresponding UserSig. Then copy the UserSig for future login.
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)
## Step 2. Download Source Code, Install Dependencies, and Run the Project
1. Clone the source code of the IM Electron demo to the local system.
```javascript
git clone https://github.com/tencentyun/im_electron_demo.git
```

2. Install project dependencies.
```javascript
// Root directory of the project
npm install

// Rendering process directory
cd src/client
npm install
```

3. Run the project.
```javascript
// Root directory of the project
npm start
```

4. Build the project.
```javascript
// Build the project in macOS
npm run build:mac
// Build the project in Windows
npm run build:windows
```



## FAQs

### What platforms are supported?
Currently, both macOS and Windows platforms are supported.

### What should I do if the error `gypgyp ERR!ERR` is reported during development environment installation?
Please see [gypgyp ERR!ERR! ](https://stackoverflow.com/questions/57879150/how-can-i-solve-error-gypgyp-errerr-find-vsfind-vs-msvs-version-not-set-from-c).

### What should I do if the screen turns white when I run `npm run start` on Mac?
The error occurs because the rendering process code is not completely built and port 3000 opened by the main process points to an empty page. The error will be resolved after the rendering process code is completely built and you refresh the window. Alternatively, you can run `cd src/client && npm run dev:react` and `npm run dev:electron` to start the rendering process and main process separately.
