## Tencentcloud-Serverless-Nodejs SDK Overview

Tencentcloud-Serverless-Nodejs is a Tencent Cloud SCF SDK that integrates SCF business flow APIs to simplify the function invocation method. It can be used to invoke a function quickly from a local system, CVM instance, container, or function, eliminating your need to encapsulate public TencentCloud APIs.

## Features
Tencentcloud-Serverless-Nodejs SDK has the following features:

* It can invoke functions in a high-performance, low-latency manner.
* It enables quick invocation across functions after the required parameters are entered (it will obtain parameters in environment variables by default, such as region and `secretId`).
* It supports access with private network domain names.
* It supports session keep-alive.
* It supports cross-region function invocation.


## Quick Start
### Preparations for development
- Development environment
Node.js 8.9 and higher.
- Operating environment
Windows, Linux, or macOS with Tencentcloud-Serverless-Nodejs SDK installed.
- You are recommended to install [SCF CLI](https://github.com/tencentyun/scfcli) to quickly deploy functions locally.

### Tencentcloud-Serverless-Nodejs SDK installation
#### Installation through npm (Recommended)
1. Select the directory path as needed and create a directory under it.
For example, you can create a project directory named `testNodejsSDK` in the `/Users/xxx/Desktop/testNodejsSDK` path.
2. Enter the `testNodejsSDK` directory and run the following commands in sequence to install the Tencentcloud-Serverless-Nodejs SDK.
```shell
npm init -y
npm install tencentcloud-serverless-nodejs
```
After installation, you can see `node_modules`, `package.json`, and `package-lock.json` in the `testNodejsSDK` directory.

#### Installation through Source Package
Go to the [GitHub code hosting page](https://github.com/TencentCloud/tencentcloud-serverless-nodejs) to download the latest source package and install it after decompression.



### Mutual function invocation
#### Samples
>
>- To make functions in different regions invoke each other, regions must be specified. For the naming convention, please see [Region List](https://intl.cloud.tencent.com/document/api/583/17238#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8).
>- If no region is specified, intra-region mutual function invocation will be used by default.
>- If no namespace is specified, `default` will be used by default.

1. <span id="Step1"></span>Create a **to-be-invoked** Node.js function named "FuncInvoked" in the region of **Beijing**. The content of the function is as follows:
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
      }) // If the SDK is running in SCF, `secretId` and `secretKey` are not required during initialization

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
The main parameters can be obtained as follows:
	- **region**: region of the **invoked** function. The Beijing region selected in [step 1](#Step1) is used as an example in this document.
	- **functionName**: name of the **invoked** function. The `FuncInvoked` function created in [step 1](#Step1) is used as an example in this document.
	- **qualifier**: version of the **invoked** function. If no version is specified, `$LATEST` will be used by default. For more information, please see [Viewing Version](https://intl.cloud.tencent.com/document/product/583/31455).
	- **namespace**: namespace of the **invoked** function. If no namespace is specified, `default` will be used by default.
	- **data**: data passed to the **invoked** function, which can be read from the `event` input parameter.
3. Create an **invoking** Node.js function named "NodejsInvokeTest" in the region of **Chengdu**. The main settings of the function are as follows:
 - Execution method: select **index.main_handler**.
 - Code submission method: select **Local zip package upload**.
    Compress all files in the `testNodejsSDK` directory in ZIP format and upload it to the cloud.
4. 
On the function details page in the [SCF Console](https://console.cloud.tencent.com/scf/list), you can test run a function by going to the function code tab and clicking **Execute**. Below is the output result:
```shell
"Already invoked a function!"
```




### Local function invocation

#### Samples

1. Create a **to-be-invoked** Node.js function named `FuncInvoked` in the **Beijing** region. The content of the function is as follows:
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
      }) // Replace them with your own `secretId` and `secretKey`
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
>`secretId` and `secretKey`: secret ID and secret key of TencentCloud API. You can go to the [CAM Console](https://console.cloud.tencent.com/cam/overview) and select **Access Key** > **API Key Management** to get them or create new ones.

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
You are recommended to run the `npm init` command to initialize the SDK before using it.
>
>- The `region`, `secretId`, and `secretKey` parameters can be passed in by using the initialization command.
>- After initialization is completed, the initialization configuration can be reused for future API calls.


**Parameter information:**

| Parameter Name | Required | Type | Description |
| :-------- | :------: | :----: | ----------------------------------------- |
| region | No | `String` | Region |
| secretId | No | `String` | `process.env.TENCENTCLOUD_SECRETID` is used by default |
| secretKey | No | `String` | `process.env.TENCENTCLOUD_SECRETKEY` is used by default |
| token | No | `String` | `process.env.TENCENTCLOUD_SESSIONTOKEN` is used by default |


<span id="Invoke"></span>
#### Invoke
This API is used to invoke a function. Currently, sync invocation is supported.

**Parameter information:**

| Parameter Name | Required | Type | Description |
| :----------- | :------: | :----: | ----------------------|
| functionName | Yes | `String` | Function name |
| qualifier | No | `String` | Function version. Default value: $LATEST |
| data | No | `String` | Input parameter for function execution |
| namespace | No | `String` | Namespace. Default value: default |
| region | No | `String` | Region |
| secretId | No | `String` | `process.env.TENCENTCLOUD_SECRETID` is used by default |
| secretKey | No | `String` | `process.env.TENCENTCLOUD_SECRETKEY` is used by default |
| token | No | `String` | `process.env.TENCENTCLOUD_SESSIONTOKEN` is used by default |


