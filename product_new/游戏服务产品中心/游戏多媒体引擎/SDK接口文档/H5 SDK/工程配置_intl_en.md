This document describes how to get started with the GME APIs for HTML5.

## Platforms Supported by the SDK for HTML5
<table>
   <tr>
      <td>OS/Platform</td>
      <td>Browser/WebView</td>
      <td>Version Requirement</td>
      <td>Remarks</td>
   </tr>
   <tr>
      <td>iOS</td>
      <td>Safari</td>
      <td>11.1.2</td>
      <td>As some bugs still emerge occasionally in Apple Safari, it is recommended to restrain from developing iOS products before Apple fixes them.</td>
   </tr>
   <tr>
      <td rowspan="2">Android</td>
      <td>TBS (the default WebView of WeChat and Mobile QQ)</td>
      <td>43600</td>
      <td>The default built-in browser kernel of WeChat and Mobile QQ is <a href="https://x5.tencent.com/">TBS</a></td>
   </tr>
   <tr>
      <td>Chrome</td>
      <td>60+</td>
      <td>H.264 support is required</td>
   </tr>
   <tr>
      <td rowspan="2">macOS</td>
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
      <td rowspan="2">Windows (PC)</td>
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

## Preparations
The SDK can be obtained in the following steps:
1. Go to the [Download Guide](https://intl.cloud.tencent.com/document/product/607/18521) page.
2. Locate the SDK resources for HTML5 on the page.
3. Click **Download** on the page.


## Frontend Project Configuration Steps
#### 1. Open ports
If you have configured a firewall for your network, be sure to open the following ports:

| Protocol | Port |
| ---- | ----------------- |
| TCP  | 8687              |
| UDP  | 8000, 8800, 443 |

Import the SDK by using CDN.

#### 2. Import frontend library files
Refer to the following code to import `WebRTCAPI.min.js` into the project. 
```
html
<script src="https://sqimg.qq.com/expert_qq/webrtc/3.0/WebRTCAPI.min.js"></script>
```


## Server-Side Deployment Steps
The use of the GME SDK requires authentication which involves keys and is not suitable for implementation on the client. You are recommended to deploy it separately.
If only client implementation is needed for the time being, please refer to the provided demo project.

#### 1. Download the program
[Download](https://main.qcloudimg.com/raw/b1d8e4d8e7321fd67250069d07bf2016.zip) the sample `authBuffer` program, which can sign the authentication information for a specified `SDKAppID`.

#### 2. Configure the server-side authentication project
Go to the `signdemo` directory and modify the `config.js` file: open the `config.js` file, delete the default configuration, and call the `appidMap` function in the place where the code is deleted (the parameters are the `SDKAppid` applied for on the Tencent Cloud backend and the corresponding authentication key).

```
const AuthBufferConfig = function () {
    this.appidMap = {};
    this.appidMap["1400089356"] = "1cfbfd2a1a03a53e";
};
// Replace 1400089356 with the `sdkAppid` applied for on the Tencent Cloud backend and replace 1cfbfd2a1a03a53e with the authentication key corresponding to the `sdkAppid`
```

>The `AuthKey` must correspond to your `SDKAppid`.

#### 3. Deploy the server-side authentication project
Go to the directory where the sample `authBuffer` program resides and run the following statement to install the dependencies:

```
npm i
```

Then, execute the `node index.js` script to run the signature service.

>As the async syntax is used, please make sure that your node is above v8. Run `node -v` on the command line to view the version.


#### 4. Test the deployment result
You can run the following command on the command line for test (make sure that your system has a `curl` command):
```
// Generate a `userSig`:
curl "http://127.0.0.1:10005/" --data "sdkappid=1400089356&roomid=1234123&openid=1234567"
```

After the signing program is executed, the authentication information will be returned as shown below:
```
{"userSig":"AqhHE7QHLFYPfV/zfyrdRYHfuUn6eOA8g/J6GMjVy//Shr5ByJPTi8hzR2KyXMvn","errorCode":0}
```
