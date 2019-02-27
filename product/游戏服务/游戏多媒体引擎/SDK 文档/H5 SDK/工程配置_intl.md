## Overview
Thank you for using Tencent Cloud Game Multimedia Engine (GME) SDK. This document describes the necessary preparations that make it easy for HTML5 developers to debug and access the APIs of GME.

## Platforms Supported by GME's HTML5 SDK
| OS | Browser/Webview | Version | Remarks |
| ------------------------- | -------- | ---------------------- |------- |
| iOS | Only Safari is supported | 11.1.2 | As Safari still has occasional bugs, it is recommended to restrain from developing iOS products with GME's HTML5 SDK before Apple fixes the bugs |
| Android | TBS (The default webview of WeChat and Mobile QQ) | 43600 | The default built-in browser kernel of WeChat and Mobile QQ is TBS. [Overview of TBS](http://x5.tencent.com/) |
| Android | Chrome | 60+ | H264 needs to be supported |
| Mac | Chrome | 47+ | |
| Mac | Safari | 11+ | |
| Windows (PC) | Chrome | 52+ | |
Windows (PC) | [QQ Browser](https://browser.qq.com/) | 10.2 | &nbsp; |


## Getting the SDK
The SDK can be obtained in the following methods.

### 1. Go to the [Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).


### 2. Find the HTML5 SDK on the page.


### 3. Click the **Download** button.


## Preparations

### 1. Open the ports

If your network has a firewall, please make sure that the following ports are open:

| Protocol | Port Number |
| ---- | ----------------- |
| TCP | 8687 |
| UDP | 8000, 8800, 443 |

Reference the SDK using CDN.
### 2. Reference WebRTCAPI.min.js on the page

```html
<script src="https://sqimg.qq.com/expert_qq/webrtc/3.0/WebRTCAPI.min.js"></script>
```

### 3. Set HTML5 authentication


## Authentication Settings

### Signing steps
To use GME, you need to sign the authentication information. Below are the steps to do so:

### Download the program
Click this link to download the provided signdemo program, which can sign the authentication information for the specified sdkappid.

### Make modifications accordingly
Go to the signdemo directory and modify the config.js file in the following way: Open the config.js file, delete the default configuration, and call the appidMap function in the place where the code is deleted. The parameters are the SDKAppid applied for in the Tencent Cloud backend and the corresponding authentication key.

```
const AuthBufferConfig = function () {
    this.appidMap = {};
    this.appidMap["1400089356"] = "1cfbfd2a1a03a53e";
};
// Replace 1400089356 with the sdkAppid applied for in the Tencent Cloud backend and 1cfbfd2a1a03a53e with the authentication key corresponding to the sdkAppid
```

>! AuthKey must correspond to the sdkAppid

### Install the npm package and run it
Go to the signdemo directory and execute the following statement to install the related dependencies:
```
npm i
```
Then, execute the script "node index.js" and run the signing service.

>! As the async syntax is used, please make sure that your node is above version 8. Execute the command "node -v" in command line to view the version.


### Testing
You can test it with the following command in command line (make sure that there is a curl directive in the system):
```
// Generate userSig:
curl "http://127.0.0.1:10005/" --data "sdkappid=1400089356&roomid=1234123&openid=1234567
(The verification can also access the website, but also needs the supported SDK app ID; 1400089356 is supported by default)
```

Return example:

```
{"userSig":"AqhHE7QHLFYPfV/zfyrdRYHfuUn6eOA8g/J6GMjVy//Shr5ByJPTi8hzR2KyXMvn","errorCode":0}
```
