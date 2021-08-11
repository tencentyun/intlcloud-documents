## Overview

- Welcome to Tencent Cloud Software Development Kit (SDK) for Node.js 4.0, a companion tool for the TencentCloud API 3.0 platform. The new SDK 4.0 is unified and features the same SDK usage, API call methods, error codes, and returned packet formats for different programming languages.
- This document takes SDK for Node.js 4.0 as an example to describe how to use the SDK with simple samples. It makes it easier for Node.js developers to debug and access Tencent Cloud product APIs.
- This version currently supports various Tencent Cloud services such as CVM, VPC, and CBS and will support more services in the future.

## Dependent Environment

- Node.js v10.0.0 and above.
- Activate your product in the [Tencent Cloud console](https://console.cloud.tencent.com/).
- Get the security credential, which consists of `SecretID` and `SecretKey`. `SecretID` is used to identify the API requester, while `SecretKey` is a key used for signature string encryption and authentication by the server. You can get them on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page as shown below:
![](https://main.qcloudimg.com/raw/bce1344cc0c9b8e8f7198ddbf2490178.png)
>!**Your security credential represents your account identity and granted permissions, which is equivalent to your login password. Do not disclose your `SecretKey` to others.**
- Get the calling address (endpoint), which is generally in the format of `\*.tencentcloudapi.com` and varies by product. For example, the endpoint of CVM is `cvm.tencentcloudapi.com`. For specific endpoints, please see the [API documentation](https://intl.cloud.tencent.com/document/api) of the corresponding product.

## Installing SDK

### Method 1. Install through npm

Installation through npm is the recommended way to use the SDK for Node.js. npm is a dependency manager for Node.js that supports the dependencies your project requires and installs them into your project. For more information, please visit [npm official website](https://www.npmjs.com/).

1. Run the following installation command:
```
npm install tencentcloud-sdk-nodejs --save
```
2. Import the corresponding module code into your code. For more information, please see the SDK sample below.
>?
>- The above import method downloads the SDKs of all Tencent Cloud products to your local system. You can replace `tencentcloud-sdk-nodejs` with a specific product SDK name such as `tencentcloud-sdk-nodejs-cvm/cbs/vpc` to import the SDK of the specific product. In the code, you can change `require("tencentcloud-sdk-nodejs")` to `require("tencentcloud-sdk-nodejs-cvm/cbs/vpc")` and keep the rest unchanged, which can greatly save the storage space. For more information, please see the sample.

### Method 2. Install through source package

1. Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-nodejs) to download the source code package.
2. Decompress the source package to an appropriate location in your project.
3. Import the corresponding module code into your code. For more information, please see the SDK sample below.

## Using SDK
### Sample

```js
const tencentcloud = require("tencentcloud-sdk-nodejs")

// Import the client models of the corresponding product module
const CvmClient = tencentcloud.cvm.v20170312.Client

const clientConfig = {
  // Tencent Cloud authentication information
  credential: {
    secretId: "secretId",
    secretKey: "secretKey",
  },
  // Product region
  region: "ap-shanghai",
  // Optional instance configuration
  profile: {
    signMethod: "HmacSHA256", // Signature algorithm
    httpProfile: {
      reqMethod: "POST", // Request method
      reqTimeout: 30, // Request timeout period in seconds, which is 60s by default
    },
  },
}
// Instantiate the client object of the requested product (with CVM as an example)
const client = new CvmClient(clientConfig)
// Call the API you want to access through the client object; you need to pass in the request object and the response callback function
client.DescribeZones().then(
  (data) => {
    console.log(data)
  },
  (err) => {
    console.error("error", err)
  }
)
```

>! During execution, you need to replace `secretId` and `secretKey` with real values.

In projects that support typescript, use the following method to call:

```js
import * as tencentcloud from "tencentcloud-sdk-nodejs"

// Import the client models of the corresponding product module
const CvmClient = tencentcloud.cvm.v20170312.Client

const clientConfig = {
  // Tencent Cloud authentication information
  credential: {
    secretId: "secretId",
    secretKey: "secretKey",
  },
  // Product region
  region: "ap-shanghai",
  // Optional instance configuration
  profile: {
    signMethod: "HmacSHA256", // Signature algorithm
    httpProfile: {
      reqMethod: "POST", // Request method
      reqTimeout: 30, // Request timeout period in seconds, which is 60s by default
    },
  },
}
// Instantiate the client object of the requested product (with CVM as an example)
const client = new CvmClient(clientConfig)
// Call the API you want to access through the client object; you need to pass in the request object and the response callback function
client.DescribeZones().then(
  (data) => {
    console.log(data)
  },
  (err) => {
    console.error("error", err)
  }
)
```

The input parameters for instantiating `Client` support the `clientConfig` data structure. For more information, please see [ClientConfig](https://github.com/TencentCloud/tencentcloud-sdk-nodejs/blob/master/src/common/interface.ts).

### More samples

For more demos, please go to the [`examples`](https://github.com/TencentCloud/tencentcloud-sdk-nodejs/tree/master/examples) directory.

## Relevant Configuration

### Proxy
If there is a proxy in your environment, you need to set the system environment variable `https_proxy`; otherwise, it may not be called normally, and a connection timeout exception will be thrown.

## Legacy SDK
We recommend you use the new version of the SDK for Node.js. If you have to use a legacy SDK, please go to the [GitHub repository](https://github.com/CFETeam/qcloudapi-sdk).
