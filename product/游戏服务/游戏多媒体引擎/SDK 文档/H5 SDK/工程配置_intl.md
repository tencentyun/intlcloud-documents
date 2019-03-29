This document provides preparations that make it easy for H5 developers to debug and integrate the APIs for Game Multimedia Engine.

## Platforms Supported by H5 SDK
<table>
   <tr>
      <td>Operating System</td>
      <td>Browser/Webview</td>
      <td>Version</td>
      <td>Notes</td>
   </tr>
   <tr>
      <td>iOS</td>
      <td>Safari</td>
      <td>11.1.2</td>
      <td>Since bugs still emerge occasionally in Apple Safari, it is recommended to restrain from developing iOS products with H5 SDK before Apple fixes the bugs.</td>
   </tr>
   <tr>
      <td rowspan="2">Android</td>
      <td>TBS (The default Webview of WeChat and Mobile QQ)</td>
      <td>43600</td>
      <td>The default built-in browser kernel in WeChat and Mobile QQ is <a href="https://x5.tencent.com/">TBS.</a></td>
   </tr>
   <tr>
      <td>Chrome</td>
      <td>60+</td>
      <td>H264 should be supported</td>
   </tr>
   <tr>
      <td rowspan="2">Mac</td>
      <td>Chrome</td>
      <td>47+</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Safari</td>
      <td>11+</td>
      <td>-</td>
   </tr>
   <tr>
      <td rowspan="2">Windows(PC)</td>
      <td>Chrome</td>
      <td>52+</td>
      <td>-</td>
   </tr>
   <tr>
      <td><a href="https://browser.qq.com/">QQ Browser</a></td>
      <td>10.2</td>
      <td>-</td>
   </tr>
</table>

## SDK Preparation
You can obtain the SDK by the following steps:
1. Go to the [Download Instructions](https://cloud.tencent.com/document/product/607/18521) page.
2. Locate the SDK resource for H5 on the page.
3. Click **Download**.


## Preparations
### 1. Open ports
If you have configured a firewall for your network, make sure you've opened the following ports:

| Protocol | Port |
| ---- | ----------------- |
| TCP | 8687 |
| UDP | 8000, 8800, and 443 |

Introduce SDK using CDN.

### 2. Introduce WebRTCAPI.min.js

```
html
<script src="https://sqimg.qq.com/expert_qq/webrtc/3.0/WebRTCAPI.min.js"></script>
```

### 3. Configure H5 authentication
#### Download the program
[Download](https://main.qcloudimg.com/raw/b1d8e4d8e7321fd67250069d07bf2016.zip) the authBuffer program sample, which can sign the authentication information for the specified sdkappid.

#### Modify as required
Go to the signdemo directory and modify the config.js file: Open the config.js file, delete the default configuration, and call the appidMap function in the place where the code is deleted. The parameters are the SDKAppid applied in Tencent Cloud backend and the corresponding authentication key.

```
const AuthBufferConfig = function () {
    this.appidMap = {};
    this.appidMap["1400089356"] = "1cfbfd2a1a03a53e";
};
// Replace 1400089356 with the sdkAppid applied in Tencent Cloud backend, and replace 1cfbfd2a1a03a53e with the authentication key corresponding to the sdkAppid
```

>! AuthKey must correspond to your sdkAppid.

#### Install and run npm package
Go to the directory where the authBuffer program sample resides, and execute the following statement to install the dependencies:

```
npm i
```

Then, execute the script "node index.js" to run the signature service.

>! As the async syntax is used, make sure your node is above version 8. Execute "node -v" in the command line to view the version.


#### Test
You can input the following command in the command line for test (make sure there is the curl command in the system):

```
// Generate userSig:
curl "http://127.0.0.1:10005/" --data "sdkappid=1400089356&roomid=1234123&openid=1234567"
```

#### Return sample

```
{"userSig":"AqhHE7QHLFYPfV/zfyrdRYHfuUn6eOA8g/J6GMjVy//Shr5ByJPTi8hzR2KyXMvn","errorCode":0}
```

