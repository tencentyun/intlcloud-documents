## Overview
Welcome to Tencent Cloud Software Development Kit (SDK) 3.0, a companion tool for the TencentCloud API 3.0 platform. Currently, it supports products such as CVM, VPC and CBS. All cloud services and products will be integrated here for access in the future. The new version of SDK is unified and features the same SDK usage, API call methods, error codes and return packet formats for different languages.
To make it easier for NODEJS developers to debug and access the APIs of Tencent Cloud products, this document describes the Tencent Cloud SDK for NODEJS and provides a simple example of using the SDK for the first time, helping you quickly get the SDK and start calling.

## API Explore
API Explore provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.

## Dependent Environment

1. NODEJS version 7.10.1 or higher.
2. Activate the corresponding product in the Tencent Cloud [Console](https://console.cloud.tencent.com/).
3. Get the SecretID, SecretKey and call address (endpoint). The general format of endpoint is *.tencentcloudapi.com. For example, the call address of CVM is cvm.tencentcloudapi.com. For details, see the documentation of the specific product.

## Installation
Obtain the security credentials before installing the SDK for NODEJS. Before using the TencentCloud API for the first time, you need to first apply for security credentials in the Tencent Cloud Console, including SecretID and SecretKey. SecretID is used to identify the API caller, while SecretKey is used to encrypt the signature string and verify it on the server. You must keep the SecretKey private and avoid disclosure.

### Installing via npm
Installing via npm, a NODEJS package management tool, is the recommended way to use the SDK for NODEJS. For more information on npm, see [npm's official website](https://www.npmjs.com/).
1. Execute the following installation command:
```
npm install tencentcloud-sdk-nodejs-intl-en --save
```

2. Refer to the corresponding module code in your code. For details, see the example.

## Example
```js
const tencentcloud = require("../../../../tencentcloud-sdk-nodejs-intl-en");

// Import the client models of the corresponding product module.
const CvmClient = tencentcloud.cvm.v20170312.Client;
const models = tencentcloud.cvm.v20170312.Models;

const Credential = tencentcloud.common.Credential;

// Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
let cred = new Credential("secretId", "secretKey");

// Instantiate the client object to request the product (with CVM as an example).
let client = new CvmClient(cred, "ap-shanghai");

// Instantiate a request object.
let req = new models.DescribeZonesRequest();

// Call the API you want to access through the client object; you need to pass in the request object and the response callback function.
client.DescribeZones(req, function(errMsg, response) {
    // The request is returned exceptionally and the exception information is printed.
    if (errMsg) {
        console.log(errMsg);
        return;
    }
    // The request is returned normally and the response object is printed.
    console.log(response.to_json_string());
});
```

## More Examples

You can find more detailed examples in the examples directory of the [GitHub](https://github.com/TencentCloud/tencentcloud-sdk-nodejs-intl-en/tree/master/examples) repository.
