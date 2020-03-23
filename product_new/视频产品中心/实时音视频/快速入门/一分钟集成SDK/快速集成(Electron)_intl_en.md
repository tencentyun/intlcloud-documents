This document describes how to quickly integrate the Tencent Cloud TRTC SDK for Electron into your project.

## Supported Platforms
-  Windows (PC)
-  macOS

## Environment Requirements

#### Windows 

Go to the [download address](https://nodejs.org/en/download/), select the Windows 32-bit version, and install the node environment.

>!`trtc-electron-sdk` currently only supports the Windows 32-bit version.

### macOS

Install node by running the following command:
```
brew install node
```

## Integrating the TRTC SDK for Electron

Make sure that your project has been integrated with Electron. Check whether `package.json` in your project directory contains the following code:
```
"devDependencies": {
	"electron": "x.x.x" // v4.0.0 or above is required
}
```

Install the SDK package by using the npm command in your Electron project:

```
npm install trtc-electron-sdk --save
```

Check whether the SDK has been successfully installed in `package.json` in the project directory:
```
"dependencies": {
    "trtc-electron-sdk": "x.x.x"
}
```
> ? The latest version of the TRTC SDK for Electron can be viewed in [trtc-electron-sdk](https://www.npmjs.com/package/trtc-electron-sdk)

Import the module into the project script and use:

```javascript
const TRTCCloud = require('trtc-electron-sdk');
this.rtcCloud = new TRTCCloud();
// Get the SDK version number
this.rtcCloud.getSDKVersion();
```

## FAQs

### 1. What are the restrictions of the firewall?

As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please see [Dealing with Organizational Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35123/35164) for assistance.
