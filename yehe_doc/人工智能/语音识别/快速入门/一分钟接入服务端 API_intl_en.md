## Overview
This document describes how to use API 3.0 Explorer to debug ASR APIs online and quickly integrate the Tencent Cloud SDK corresponding to the APIs into your local project.

## Directions
### Activate ASR service
Before calling ASR APIs, you should access the [ASR console](https://console.cloud.tencent.com/asr) to complete identity verification and face recognition. Then, read the User Agreement, select "I have read and agree to the User Agreement", and click **Activate Now** to activate **APIs for recording file recognition, real-time speech recognition, one-sentence recognition, ultrafast recording file recognition, and async audio stream recognition services**. If you need to activate the business license verification or VAT invoice verification feature, you can go to the service overview page to apply for activation, and the service can be used after approval. 
![](https://main.qcloudimg.com/raw/284e58e4eaed33b3ea9e290b0872f920.png)

After the service is successfully activated, you will get the free tiers of calls for each service, which can be viewed on the [Resource Package Management](https://console.cloud.tencent.com/asr/resourcebundle) page. In addition, you can also purchase resource packages for various speech recognition service on the [ASR purchase](https://buy.cloud.tencent.com/asr) page. After the free tiers and number of resource package calls are used up, API calls will be billed in the pay-as-you-go mode and settled monthly or daily. For specific billing standards, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1118/43352).

### Debugging ASR APIs
After the ASR service is successfully activated, go to the ASR [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=asr&Version=2019-06-14&Action=CreateAsyncRecognitionTask&SignVersion=) online API debugging page, select the API to be called, and enter the **input parameters**. You can view the specific descriptions of input parameters in the **Parameter Description** tab on the API 3.0 Explorer UI.
>?The platform will provide a temporary `Access Key` to the logged-in user for debugging.

![](https://main.qcloudimg.com/raw/32372679d9f39b46009ec5eaebb302d5.png)

After entering the **input parameters**, select the **Code Generation** tab, and you can see the automatically generated code in different programming languages (Java, Python, Node.js, PHP, Go, .NET, and C++), and some fields in the generated code are related to the entered content. If you need to adjust the input parameters, you can regenerate the code after modifying the parameter values on the left.
![](https://main.qcloudimg.com/raw/d2c7cdbf68df6d975bf538babb70b0ba.png)
Select the **Online Call** tab and click **Send Request** to make a real request for your debugging and reference.
![](https://main.qcloudimg.com/raw/2822cfaacc45d821ea57375409740ace.png)

### Integrating ASR SDK
Confirm that your local dependent environment meets the following requirements:

| Programming Language | SDK Integration Requirements |
|---------|---------|
| Node.js | Node.js 10.0.0 and above |
| Python | Python 2.7 or 3.6–3.9 |
| Java | JDK 7 and above |
| Go | Go 1.9 and above (or Go 1.14 if go.mod is used) |
| .NET | .NET Framework 4.5+ or .NET Core 2.1 |
| PHP | PHP 5.6.0 and above |
| C++ | Compiler for C++ 11 or above, i.e., GCC 4.8 or above (currently, only the Linux installation environment is supported, while Windows is not) |
| Ruby | Ruby 2.3 and above |

Install the Tencent Cloud ASR SDK corresponding to the local dependent environment. The following takes Node.js as an example to describe the SDK installation and use methods. For the SDK use methods in other languages, see [Tencent Cloud SDK User Manual](https://cloud.tencent.com/document/sdk).

#### Installation through npm (recommended)
Installation through npm is the recommended way to use the SDK for Node.js. npm is a dependency manager for Node.js that supports the dependencies your project requires and installs them into your project. For more information, visit [npm's official website](https://www.npmjs.com/).
1. Run the following installation command:
```
npm install tencentcloud-sdk-nodejs --save
```
2. Import the corresponding module code in your code. For more information, see the sample code.
3. The above import method downloads the SDKs of all Tencent Cloud products to your local system. You can replace `tencentcloud-sdk-nodejs` with a specific product SDK name such as `tencentcloud-sdk-nodejs-cvm/cbs/vpc` to import the SDK of the specific product. In the code, you can change `require("tencentcloud-sdk-nodejs")` to `require("tencentcloud-sdk-nodejs-cvm/cbs/vpc")` and keep the rest unchanged, which can greatly save the storage space. For more information, see the sample.

#### Installation through source package
1. Go to the [GitHub code hosting page](https://github.com/TencentCloud/tencentcloud-sdk-nodejs) or [quick download address](https://github.com/TencentCloud/tencentcloud-sdk-nodejs/archive/refs/heads/master.zip) to download the source code package.
2. Decompress the source package to an appropriate location in your project.
3. Import the corresponding module code in your code. For more information, see the sample code.

### Demo
After the SDK installation is completed, you can import the code automatically generated by API 3.0 Explorer into your project. Taking Node.js as an example, a simple demo is as follows:

```
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
// Instantiate the client object to request the product (with CVM as an example).
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

In projects that support typescript, use the following method to call:

```
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
// Instantiate the client object to request the product (with CVM as an example).
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
The input parameters for instantiating `Client` support the `clientConfig` data structure. For more information, see [ClientConfig](https://github.com/TencentCloud/tencentcloud-sdk-nodejs/blob/master/src/common/interface.ts).

