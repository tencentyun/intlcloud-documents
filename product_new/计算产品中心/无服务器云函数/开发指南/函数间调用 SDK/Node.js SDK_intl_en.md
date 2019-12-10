## Tencentcloud-Serverless-Nodejs SDK Overview

Tencentcloud-Serverless-Nodejs is a Tencent Cloud SCF SDK that integrates SCF business flow APIs to simplify the invoke function. Users can invoke a function quickly from a local system, CVM instance, container or function, eliminating the need to encapsulate APIs in a public cloud.

## Features
Tencentcloud-Serverless-Nodejs SDK has the following features:

* It can invoke functions in a high-performance, low-latency manner.
* It enables quick invocation across functions after the required parameters are entered (it will obtain parameters in environment variables by default, such as region and secretId).
* It supports access with private network domain names.
* It supports session keep-alive.
* It supports cross-region function invocation.


## Quick Start
### Preparing for development
- Development environment
Node.js 8.9 or a higher version has been installed.
- Operating environment
Windows, Linux, or macOS with tencentcloud-serverless-nodejs SDK have been installed.
- We recommend that you install [SCF CLI](https://github.com/tencentyun/scfcli) to deploy local functions rapidly.

### Installing the tencentcloud-serverless-nodejs SDK
#### Installing via npm (recommend)
1. Select the directory path as needed and create a directory under it.
For example, you can create a project directory named `testNodejsSDK` in the `/Users/xxx/Desktop/testNodejsSDK` path.
2. Enter the `testNodejsSDK` directory and run the following commands in sequence to install tencentcloud-serverless-nodejs SDK.
```shell
npm init -y
npm install tencentcloud-serverless-nodejs
```
After installation, you can see `node_modules`, `package.json`, and `package-lock.json` in the `testNodejsSDK` directory.

#### Installing via source package
Go to the [GitHub code hosting page](https://github.com/TencentCloud/tencentcloud-serverless-nodejs) to download the latest source package and install it after decompression.



### Chaining functions
#### Example
>
>- To chain functions in different regions, you must specify regions. For naming rules, see [Region List](https://intl.cloud.tencent.com/document/product/583/17238#Region-List).
>- If no region is specified, functions will be chained within the same region by default.
>- If no namespace is specified, `default` will be used by default.

1. Create a **to-be-invoked** Node.js function named "FuncInvoked" in the region of **Beijing**. The content of the function is as follows:
```js
'use strict';
exports.main_handler = async (event, context, callback) => {
      console.log("\n Hello World from the function being invoked\n")
      console.log(event)
      console.log(event["non-exist"])
      return event
};
```
2. Create an `index.js` file in the `testNodejsSDK` directory and enter the following sample code to create an **invoking** Node.js function.
```js
const sdk = require('tencentcloud-serverless-nodejs')
exports.main_handler = async (event,context,callback)=>{
      sdk.init({
          region: 'ap-beijing'
      }) // If the SDK is running in SCF, secretId and secretKey are not required during initialization

      console.log('prepare to invoke a function!')
      const res = await sdk.invoke({
          functionName: 'FuncInvoked',
          qualifier: '$LATEST',
          data: JSON.stringify({
              key:'value'
          }),
          namespace:'default'
      })
      console.log(res)
      //return res
      return 'Already invoked a function!'
}
```
3. Create an **invoking** Node.js function named "NodejsInvokeTest" in the region of **Chengdu**. The main settings of the function are as follows:
 - Execution method: Select **index.main_handler**.
 - Code submission method: Select **Local zip package upload**.
    Compress all files in the `testNodejsSDK` directory to ZIP format and upload them to the cloud.
4. 
On the function details page in [SCF Console](https://console.cloud.tencent.com/scf/list), you can test run a function by going to the function code sub-page and clicking **Execute**. The output is as follows:
```shell
"Already invoked a function!"
```




### Invoking a function locally

#### Example

1. Create a **to-be-invoked** Node.js function named "FuncInvoked" in the region of **Beijing**. The content of the function is as follows:
```js
'use strict';
exports.main_handler = async (event, context, callback) => {
      console.log("\n Hello World from the function being invoked\n")
      console.log(event)
      console.log(event["non-exist"])
      return event
};
```

2. Create an `index.js` file in the `testNodejsSDK` directory as an **invoking** Node.js function and enter the following sample code:
```js
const sdk = require('tencentcloud-serverless-nodejs')
exports.main_handler = async (event, context, callback) => {
      sdk.init({
          region: 'ap-beijing',
         secretId: 'AKxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxj',
          secretKey: 'WtxxxxxxxxxxxxxxxxxxxxxxxxxxxxqL'
      }) // Replace with your own secretId and secretKey
      console.log('prepare to invoke a function!')
      const res = await sdk.invoke({
          functionName: 'FuncInvoked',
          qualifier: '$LATEST',
          data: JSON.stringify({
              key:'value'
          }),
          namespace:'default'
      })
      console.log(res)
      //return res
      console.log('Already invoked a function!')
  }
  if (process.env.NODE_ENV === 'development') {
      const event = {
          test: '123'
      }
      exports.main_handler(event)
}
```
>secretId and secretKey: Secret ID and secret key of TencentCloud API. You can obtain them or create new ones by logging into the [CAM Console](https://console.cloud.tencent.com/cam/overview) and selecting **Access Key** > **API Key Management**.

3. Go to the directory where the `index.js` file is located and run the following command to view the result.
 - On Linux or macOS, run the following command:
```shell
export NODE_ENV=development && node index.js
```
 - On Windows, run the following command:
```shell
set NODE_ENV=development && node index.js
```

 The output is as follows:
```shell
prepare to invoke a function!
{"key":"value"}
Already invoked a function!
```


## API List
### API Reference
- [Init](#Init)
- [Invoke](#Invoke)

<span id="Init"></span>
#### Init
We recommend you run the `npm init` command to initialize the SDK before using it.
>
>- The `region`, `secretId`, and `secretKey` parameters can be passed in using the initialization command.
>- After completing the initialization, you can reuse the initialization configuration for future API calls.


**Parameter information:**

| Parameter Name | Required | Type | Description |
| :-------- | :------: | :----: | ----------------------------------------- |
| region | No | `String` | Region |
| secretId | No | `String` | process.env.TENCENTCLOUD_SECRETID is used by default |
| secretKey | No | `String` | process.env.TENCENTCLOUD_SECRETKEY is used by default |
| token | No | `String` | process.env.TENCENTCLOUD_SESSIONTOKEN is used by default |


<span id="Invoke"></span>
#### Invoke
This is used to invoke a function. Currently, sync invocation is supported.

**Parameter information:**

| Parameter Name | Required | Type | Description |
| :----------- | :------: | :----: | ----------------------|
| functionName | Yes | `String` | Function name |
| qualifier | No | `String` | Function version. Default value: $LATEST |
| data | No | `String` | Input parameter for function execution |
| namespace | No | `String` | Namespace. Default value: default |
| region | No | `String` | Region |
| secretId | No | `String` | process.env.TENCENTCLOUD_SECRETID is used by default |
| secretKey | No | `String` | process.env.TENCENTCLOUD_SECRETKEY is used by default |
| token | No | `String` | process.env.TENCENTCLOUD_SESSIONTOKEN is used by default |


