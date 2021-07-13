## Preparations for Development
Before installing the SDK for Node.js and using TencentCloud API for the first time, you need to apply for security credentials in the Tencent Cloud console, which consists of `SecretId` and `SecretKey`. `SecretId` is used to identify the API requester, while `SecretKey` is a key used for signature string encryption and authentication by the server. Please keep your `SecretKey` private and do not disclose it to others.

### Development environment
Node.js v8.9

### Installation through npm
Installation through npm is the recommended way to use the SDK for Node.js. npm is a dependency manager for Node.js that supports the dependencies your project requires and installs them into your project. For more information, please visit [npm's official website](https://www.npmjs.com/).
1. Run the following installation command:
```
npm install tencentcloud-sdk-nodejs --save
```
2. Refer to the corresponding module code in your code. For more information, please see the sample.

### Installation through source package
1. Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-nodejs) to download the source code package.
2. Decompress the source package to an appropriate location in your project.
3. Import the corresponding module code into your code. For more information, please see the sample.

## API List
| API Name | Description |
| :--- | :------------------------------------ |
| [CreateFunction](https://intl.cloud.tencent.com/document/api/583/18586) | Creates function |
| [DeleteFunction](https://intl.cloud.tencent.com/document/api/583/18585) | Deletes function |
| [GetFunction](https://intl.cloud.tencent.com/document/api/583/18584) | Gets function details |
| [GetFunctionLogs](https://intl.cloud.tencent.com/document/api/583/18583) | Gets function execution logs |
| [Invoke](https://intl.cloud.tencent.com/document/api/583/17243) | Executes function |
| [ListFunctions](https://intl.cloud.tencent.com/document/api/583/18582) | Gets function list |
| [UpdateFunctionCode](https://intl.cloud.tencent.com/document/api/583/18581) | Updates function code |
| [UpdateFunctionConfiguration](https://intl.cloud.tencent.com/document/api/583/18580) | Updates function configuration |

## Samples
```
'use strict';

const tencentcloud = require("/var/user/tencentcloud-sdk-nodejs");
const Credential = tencentcloud.common.Credential;

// Import the client models of the corresponding product module
const ScfClient = tencentcloud.scf.v20180416.Client;
const models = tencentcloud.scf.v20180416.Models;

exports.main_handler = (event, context, callback) => {
    console.log("Hello World")
    console.log(event)
    // console.log(context)
    callback(null, event); 

    // Instantiate an authentication object. The Tencent Cloud account `secretId` and `secretKey` need to be passed in as the input parameters
    let cred = new Credential("AKIxxxxxxPDpqj3C", "75rxxxxxxyJSODrMkx");

     // Instantiate the client object to request the product and the region where the function is located
    let client = new ScfClient(cred, "ap-shanghai");


    / / Instantiate a request object to get the function list
    console.log("Start ListFunctions")
    let req = new models.ListFunctionsRequest();
    // Call the API you want to access through the client object; you need to pass in the request object and the response callback function
    client.ListFunctions(req, function(err, response) {
        // The request returns an exception and the exception information is printed
        if (err) {
          console.log(err);
         return;
        }
        // The request is returned normally, and the `response` object is printed
        console.log(response.to_json_string());
    });

    // Instantiate a request object and call `invoke()`
    console.log("Start Invoke")
    let request = new models.InvokeRequest();
    // API parameter. Enter the name of the function to be invoked, `RequestResponse` (sync), and `Event` (async)
    let params = '{"FunctionName":"test_python", "InvocationType":"RequestResponse"}'
    request.from_json_string(params);  
    // Call the API you want to access through the client object; you need to pass in the request object and the response callback function
    client.Invoke(request, function(err, response) {
        // The request returns an exception and the exception information is printed
        if (err) {
          console.log(err);
         return;
        }
        // The request is returned normally, and the `response` object is printed
        console.log(response.to_json_string());
    },"test_python","RequestResponse");

};

```
## Packaging and Deployment
If you need to deploy a function in the SCF console and use the SDK to invoke other functions, you need to package the `tencentcloud` library and function code together into a zip file.

- Please note that the execution method specified when the function is created in the console must correspond to the code file and execution function in the zip file.
- If the generated zip package is larger than 50 MB, it should be uploaded through COS.
- The default call rate limit for TencentCloud API is 20 calls per second. If you need to increase the limit for high concurrence, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) for application.

## Related Information
You can also use Tencent SCF SDK (Tencentserverless SDK), which integrates SCF business flow APIs to simplify the function invocation method and eliminates your need to encapsulate public TencentCloud APIs. For more information, please see [Calling SDK Across Functions](https://intl.cloud.tencent.com/document/product/583/32747).
