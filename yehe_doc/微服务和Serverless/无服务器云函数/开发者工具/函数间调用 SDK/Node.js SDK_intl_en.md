## Tencentcloud-Serverless-Nodejs SDK Overview

Tencentcloud-Serverless-Nodejs is a Tencent Cloud SCF SDK that integrates SCF APIs to simplify the function invocation method. It can invoke a function from a local system, CVM instance, container, or another cloud function, eliminating the need for you to encapsulate TencentCloud APIs.

## Features
Tencentcloud-Serverless-Nodejs SDK has the following features:

* Invokes functions in a high-performance, low-latency manner
* It enables quick invocation across functions after the required parameters are entered (by default, it will obtain parameters in environment variables such as `region` and `secretId`).
* Supports access with private network domain names.
* Supports session keep-alive.
* Supports cross-region function chaining.

>? Calling SDK across functions is only applicable to event-triggered functions. HTTP-triggered functions can be invoked by requesting the corresponding path of the function in the function code.


## Getting Started
### Development Preparations
- Development environment
Node.js 8.9 or a higher version has been installed.
- Running environment
Windows, Linux, or macOS with tencentcloud-serverless-nodejs SDK have been installed.
- We recommend you use the [Serverless Cloud Framework](https://intl.cloud.tencent.com/document/product/583/32743) to quickly deploy local functions.

### Installing the tencentcloud-serverless-nodejs SDK
#### Installing via npm (recommended)
1. Select the directory path according to your actual needs and create a directory under it.
For example, you can create a project directory named `testNodejsSDK` in the `/Users/xxx/Desktop/testNodejsSDK` path.
2. Enter the `testNodejsSDK` directory and run the following commands in sequence to install tencentcloud-serverless-nodejs SDK.
```shell
npm init -y
npm install tencentcloud-serverless-nodejs
```
After installation, you will be able to see `node_modules`, `package.json`, and `package-lock.json` in the `testNodejsSDK` directory.

#### Installing via the source package
Go to the [GitHub code hosting page](https://github.com/TencentCloud/tencentcloud-serverless-nodejs) to download the latest source package and install it after decompression.

#### Using SCF to install dependencies online
To [install dependencies online with SCF](https://intl.cloud.tencent.com/document/product/583/38105), run the following command in `package.json`:
```js
{
    "dependencies": {
    "tencentcloud-serverless-nodejs":"*"
  }
}
```


### Mutual Recursion
#### Sample
>!
>- To implement mutual recursion of functions in different regions, you need to specify the region. For the naming rules, please see [Region List](https://www.tencentcloud.com/document/api/583/17238).
>- If no region is specified, functions will invoke one another within the same region.
>- If no namespace is specified, `default` will be used by default.
>- The invoker function should have the public network access enabled.
>- If parameters such as `secretId` and `secretKey` are not manually passed in, the function needs to be bound to a role with `SCF Invoke` permissions (or containing `SCF Invoke`, such as `SCF FullAccess`). For more information, please see [Roles and Policies](https://intl.cloud.tencent.com/document/product/583/38176).


1. [](id:Step1)Create a **to-be-invoked** Node.js function named "FuncInvoked" in the region of **Beijing**. The content of the function is as follows:
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
<dx-codeblock>
:::  js
const { SDK, LogType }  = require('tencentcloud-serverless-nodejs')
exports.main_handler = async (event, context) => {
    context.callbackWaitsForEmptyEventLoop = false
    const sdk = new SDK({
    region:'ap-beijing'
    }) // If you bind and run in SCF an execution role with SCF invocation permissions, the authentication information in the environment variable will be used by default
    const res = await sdk.invoke({
    functionName: 'FuncInvoked',
    logType: LogType.Tail,
    data: {
      name: 'test',
      role: 'test_role'
    }
    })
    console.log(res)
    // return res
}
:::
</dx-codeblock>

 The main parameters can be obtained as described below:
 - **region**: the region of the **invoked** function. The Beijing region selected in [step 1](#Step1) is used as an example in this document.
 - **functionName**: the name of the **invoked** function. The `FuncInvoked` function created in [step 1](#Step1) is used as an example in this document.
 - **qualifier**: the version of the **invoked** function. If no version is specified, `$LATEST` will be used by default. For more information, please see [Viewing a Version](https://intl.cloud.tencent.com/document/product/583/31455).
 - **namespace**: the namespace of the **invoked** function. If no namespace is specified, `default` will be used by default.
 - **data**: the data passed to the **invoked** function, which can be read from the `event` input parameter.
3. Create an **invoking** Node.js function named "NodejsInvokeTest" in the **Chengdu** region. The main settings of the function are as follows:
 - Execution method: Select **index.main_handler**.
 - Code submission method: Select **Local zip package upload**.
    Compress all files in the `testNodejsSDK` directory to ZIP format and upload them to the cloud.
4.  
In the [SCF console](https://console.cloud.tencent.com/scf/list), click the function just created, go to **Function management** > **Edit codes**. Click **Test** to run the function. The result should be as follows: 
```shell
"Already invoked a function!"
```

### Invoking a function locally

#### Sample

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
<dx-codeblock>
:::  js
const { SDK, LogType }  = require('tencentcloud-serverless-nodejs')
exports.main_handler = async (event, context) => {
    context.callbackWaitsForEmptyEventLoop = false
    const sdk = new SDK({
    region:'ap-beijing',
    secretId: 'AKxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxj',
    secretKey: 'WtxxxxxxxxxxxxxxxxxxxxxxxxxxxxqL'
    }) // If you bind and run in SCF an execution role with SCF invocation permissions, the authentication information in the environment variable will be used by default
    const res = await sdk.invoke({
    functionName: 'FuncInvoked',
    logType: LogType.Tail,
    data: {
      name: 'test',
      role: 'test_role'
    }
    })
    console.log(res)
    // return res
}
:::
</dx-codeblock>
<dx-alert infotype="notice" title="">
secretId and secretKey: Secret ID and secret key of TencentCloud API. You can obtain them or create new ones by logging into the [CAM Console](https://console.cloud.tencent.com/cam/overview) and selecting **Access Key** > **API Key Management**.
</dx-alert>
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

[](id:Init)
#### Init
We recommend you run the `npm init` command to initialize the SDK before using it.
>?
>- The `region`, `secretId`, and `secretKey` parameters can be passed in using the initialization command.
>- After the initialization is completed, the initialization configuration can be reused for future API calls.


**Parameter information:**

| Parameter Name | Required | Type | Description |
| :-------- | :------: | :----: | ----------------------------------------- |
| region | No | `String` | Region |
| secretId | No | `String` | process.env.TENCENTCLOUD_SECRETID is used by default |
| secretKey | No | `String` | `process.env.TENCENTCLOUD_SECRETKEY` is used by default |
| token | No | `String` | process.env.TENCENTCLOUD_SESSIONTOKEN is used by default |


[](id:Invoke)
#### Invoke
This is used to invoke a function. Currently, sync invocation is supported.

**Parameter information:**

| Parameter Name | Required | Type | Description |
| :----------- | :------: | :----: | ----------------------|
| functionName | Yes | String | Function name |
| qualifier | No | String | Function version. Default value: $LATEST |
| data | No | String | Input parameter for function execution |
| namespace |  No | String | Namespace, which is `default` by default. | 
| region | No | String | Region |
| secretId | No | String | process.env.TENCENTCLOUD_SECRETID is used by default |
| secretKey | No | String | `process.env.TENCENTCLOUD_SECRETKEY` is used by default |
| token | No | `String` | process.env.TENCENTCLOUD_SESSIONTOKEN is used by default |


