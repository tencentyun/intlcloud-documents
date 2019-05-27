## Preparations for Development
You need to obtain the security credentials before installing the SDK for Node.js. Before using the Cloud API for the first time, you need to first apply for security credentials in the Tencent Cloud Console, including SecretId and SecretKey. SecretId is used to identify the API caller, while SecretKey is used to encrypt the signature string and verify it on the server. You must keep the SecretKey private and avoid disclosure.

### Development Environment
Node.js v8.9

### Installing via npm
Installing via npm, a Node.js package management tool, is the recommended way to use the SDK for Node.js. For more information on npm, see [npm's official website](https://www.npmjs.com/).
1. Execute the following installation command:
```
npm install tencentcloud-sdk-nodejs --save
```
2. Refer to the corresponding module code in your code. For details, see the example.

### Installing via Source Package
1. Go to the [Github code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-nodejs) to download the source code package.
2. Decompress the package to an appropriate location for your project.
3. Refer to the corresponding module code in your code. For details, see the example.

## API List
| API name | Description |
| :--- | :------------------------------------ |
| [CreateFunction](https://cloud.tencent.com/document/api/583/18586) | Create a function |
| [DeleteFunction](https://cloud.tencent.com/document/api/583/18585) | Delete a function |
| [GetFunction](https://cloud.tencent.com/document/api/583/18584) | Get function details |
| [GetFunctionLogs](https://cloud.tencent.com/document/api/583/18583) | Get function execution logs |
| [Invoke](https://cloud.tencent.com/document/api/583/17243) | Execute a function |
| [ListFunctions](https://cloud.tencent.com/document/api/583/18582) | Get a function list |
| [UpdateFunctionCode](https://cloud.tencent.com/document/api/583/18581) | Update function code |
| [UpdateFunctionConfiguration](https://cloud.tencent.com/document/api/583/18580) | Update function configuration |

## Sample
```
'use strict';

const tencentcloud = require("/var/user/tencentcloud-sdk-nodejs");
const Credential = tencentcloud.common.Credential;

// Import the client models of the corresponding product module.
const ScfClient = tencentcloud.scf.v20180416.Client;
const models = tencentcloud.scf.v20180416.Models;

exports.main_handler = (event, context, callback) => {
    console.log("Hello World")
    console.log(event)
    // console.log(context)
    callback(null, event); 

    // Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
    let cred = new Credential("AKIDqeHm8Jn8mEYhgWkhOwJUUj4KQPDpqj3C", "75rRuGRSHtKvTwMgsvnwxmTyJSODrMkx");

     // Instantiate the client object to request the product and the region where the function is located
    let client = new ScfClient(cred, "ap-shanghai");


    / / Instantiate a request object to get the function list
    console.log("Start ListFunctions")
    let req = new models.ListFunctionsRequest();
    // Call the API you want to access through the client object; you need to pass in the request object and the response callback function.
    client.ListFunctions(req, function(err, response) {
        // The request returns an exception and the exception information is printed.
        if (err) {
          console.log(err);
         return;
        }
        // The request is returned normally and the response object is printed.
        console.log(response.to_json_string());
    });

    // Instantiate a request object and call invoke()
    console.log("Start Invoke")
    let request = new models.InvokeRequest();
    // API parameter. Enter the name of the function to be called, RequestResponse (sync), and Event (async)
    let params = '{"FunctionName":"test_python", "InvocationType":"RequestResponse"}'
    request.from_json_string(params);  
    // Call the API you want to access through the client object; you need to pass in the request object and the response callback function.
    client.Invoke(request, function(err, response) {
        // The request returns an exception and the exception information is printed.
        if (err) {
          console.log(err);
         return;
        }
        // The request is returned normally and the response object is printed.
        console.log(response.to_json_string());
    },"test_python","RequestResponse");

};

```
## Packaging and Deployment
If you need to deploy a function in the SCF console and use the SDK to call other functions, you need to package the tencentcloud library and function code together into a zip file.

- Please note that the execution method specified when the function is created in the console has to correspond to the code file and execution function in the zip file.
- If the generated zip package is larger than 5 MB, it should be uploaded via COS. This file size restriction on the SCF platform will be removed soon.
- The default request frequency through TencentCloud API is limited to 20 times per second. If you need to increase the limit for high concurrency, please apply by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1).
