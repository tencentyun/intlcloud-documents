Currently, the following versions of Node.js programming language are supported:
* Node.js 6.10
* Node.js 8.9
* Node.js 10.15
* Node.js 12.16

## Function Form

The Node.js function form is generally as follows:
- Node.js 10.15 and 12.16
```
module.exports = (event,context,callback)=>{
	console.log(event);
	callback(null, {code:0});
}
```
Or
```
module.exports = async (event,context)=>{
    console.log(event);
	return { code:0 };
}
```
- Node.js 8.9 and 6.10
```
exports.main_handler = (event, context, callback) => {
    console.log("Hello World");
    console.log(event);
    console.log(context);
    callback(null, event); 
};
```

## Execution Method

When you create an SCF function, you need to specify an execution method. If the Node.js programming language is used, the execution method is similar to `index.main_handler`, where `index` indicates that the executed entry file is `index.js`, and `main_handler` indicates that the executed entry function is `main_handler`. When submitting the zip code package by uploading the zip file locally or through COS, please make sure that the root directory of the package contains the specified entry file, the file contains the entry function specified by the definition, and the names of the file and function match those entered in the trigger; otherwise, execution will fail as the entry file or entry function cannot be found.

## Input Parameters

The input parameters in the Node.js environment include `event`, `context`, and `callback`, where `callback` is optional.
* **event**: this parameter is used to pass the trigger event data.
* **context**: this parameter is used to pass runtime information to your handler.
* **callback**: this parameter is used to return the desired information to the invoker in Node.js 8.9 and 6.10, which is optional. In Node.js 10.15 and 12.16, async entry functions use the `return` keyword for return, while non-async entry functions use the `callback` input parameter for return.

## Return and Exception

Your handler can use the `callback` input parameter or the `return` keyword in the code to return information. The support conditions for using `callback` or `return` for return are as follows:

<table>
<thead>
<tr>
<th>Node.js Version</th>
<th>Callback</th>
<th>Return</th>
</tr>
</thead>
<tbody><tr>
<td>6.10</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>8.9</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>10.15</td>
<td rowspan=2>Non-async entry function</td>
<td rowspan=2>Async entry function</td>
</tr>
<tr>
<td>12.16</td>
</tr>
</tbody></table>

- If `callback` is used for return, the syntax will be as follows:
```
callback(Error error, Object result);
```
	- **error**: this is an optional parameter, which is used to return the error content when function execution fails internally. It can be set to `null` in case of success.
	- **result**: this is used to return the successful execution result information of the function, which is optional. This parameter needs to be compatible with `JSON.stringify` for serialization to JSON format.
- If the `return` keyword is used for return, you can directly use `return object` to return an object or value.
- If `callback` or `return` is not invoked in the code, the SCF backend will make the invocation implicitly and return `null`.

The return value will be handled differently depending on the type of invocation when the function is invoked. The return value of a sync invocation will be serialized to JSON format and then returned to the invoker, while the return value of an async invocation will be discarded. In addition, the return value will be displayed at the `ret_msg` position in the function log for both sync and async invocations.


## Async Attribute of Node.js 10.15 and 12.16

In the runtime of Node.js 10.15 and 12.16, sync execution return and async event processing can be performed separately:
* After the sync execution process of an entry function is completed and the result is returned, function invocation will immediately return its result, and the return information in the code will be send to the function invoker.
* After the sync process is completed and the result returned, the async logic in the code will continue to be executed and processed. The actual function execution process ends and exits only when the async event is completely executed.

>!
>- SCF logs are collected and processed after the entire execution process ends. Therefore, before the sync execution process is completed and the result is returned, logs and operation information such as time used and memory utilization cannot be provided in the SCF return information. You can query the detailed information in logs by using `Request Id` after the actual function execution process is completed.
>- The function execution duration is calculated based on the async event execution duration. If the async event queue cannot get empty or its execution cannot be completed, function timeout will occur. In this case, the invoker may have received the correct response result of the function, but the execution status of the function will still be marked as failure due to timeout, and the timeout period will be calculated as the execution duration.

The sync and async execution attributes, return time, and execution duration in Node.js 10.15 and 12.16 are as shown below:
![node10.15feature](https://main.qcloudimg.com/raw/bdd1744107f3cce044d596afe7b230cf.png)

### Async attribute sample of Node.js 10.15 or 12.16 function

Use the following sample code to create a function, where the `setTimeout` method is used to set a function that will be executed in 2 seconds:
```
'use strict';
exports.main_handler = (event, context, callback) => {
    console.log("Hello World")
    console.log(event)
    setTimeout(timeoutfunc, 2000, 'data');
    callback(null, event); 
};

function timeoutfunc(arg) {
    console.log(`arg => ${arg}`);
}
```
After saving the code, you can invoke this function through the testing feature in the console or the `Invoke` API. You can see that the function can return the result in a response period below 1 second.
You can see the following statistics in the function execution log:
```
START RequestId: 1d71ddf8-5022-4461-84b7-e3a152403ffc
Event RequestId: 1d71ddf8-5022-4461-84b7-e3a152403ffc
2020-03-18T09:16:13.440Z	1d71ddf8-5022-4461-84b7-e3a152403ffc	Hello World
2020-03-18T09:16:13.440Z	1d71ddf8-5022-4461-84b7-e3a152403ffc	{ key1: 'test value 1', key2: 'test value 2' }
2020-03-18T09:16:15.443Z	1d71ddf8-5022-4461-84b7-e3a152403ffc	arg => data 
END RequestId: 1d71ddf8-5022-4461-84b7-e3a152403ffc
Report RequestId: 1d71ddf8-5022-4461-84b7-e3a152403ffc Duration:2005ms Memory:128MB MemUsage:13.425781MB
```
A 2,005-ms execution period is logged. You can also find in the log that the `arg => data` is output 2 seconds later, which shows that the relevant async operations are executed in the current invocation after the execution of the sync process is completed, while function invocation ends after execution of the async task is completed.

## Support for Async Events in Node.js 8.9 and 6.10
Both Node.js 8.9 and 6.10 support async events; however, immediate return after sync processing is completed is not supported. After the callback is invoked in the entry function, the SCF backend will wait until processing of async events is completed and the event queue gets empty before returning the result for the function invocation and ending this invocation.

Therefore, for the following code:
```
'use strict';

exports.callback_handler = function(event, context, callback) {
    console.log("event = " + event);
    console.log("before callback");
    setTimeout(
        function(){
            console.log(new Date);
            console.log("timeout before callback");
        }, 
        500
    );
    callback(null, "success callback");
    console.log("after callback");
};
```
The actual log output is:
```
2018-06-14T08:07:16.545Z	f3cb1ef4-6fa9-11e8-aa8a-525400c7c826	event = [object Object]
2018-06-14T08:07:16.546Z	f3cb1ef4-6fa9-11e8-aa8a-525400c7c826	before callback
2018-06-14T08:07:16.546Z	f3cb1ef4-6fa9-11e8-aa8a-525400c7c826	after callback
2018-06-14T08:07:17.047Z	f3cb1ef4-6fa9-11e8-aa8a-525400c7c826	2018-06-14T08:07:17.047Z
2018-06-14T08:07:17.048Z	f3cb1ef4-6fa9-11e8-aa8a-525400c7c826	timeout before callback
```

As you can see, the async task set by `setTimeout` is executed after the callback is executed, and the function does not actually return until the async task is completed.


## Disabling Event Loop Wait

Some externally referenced libraries may cause the event loop to never get empty, which may lead to timeout due to failed return of the function in some cases. In order to avoid the impact of external libraries, you can control the function return timing by turning off event loop wait. You can modify the default callback behavior in the following way to avoid waiting for the event loop to get empty.
* Set `context.callbackWaitsForEmptyEventLoop` to `false`.
By setting `context.callbackWaitsForEmptyEventLoop = false;` before the `callback` callback is executed, the SCF backend can freeze the process immediately after the `callback` callback is invoked and return immediately after the sync process is completed without waiting for the event in the event loop.

## Log

You can use the following statements in the program to output a log:

* console.log()
* console.error()
* console.warn()
* console.info()

The output can be viewed at the `log` location in the function log.

## Installing Dependencies

For more information, please see [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879) and [Online Dependency Installation](https://intl.cloud.tencent.com/document/product/583/38105).

## Included Libraries and Usage

### COS SDK

SCF's runtime environment already contains the [COS SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/8629), and the specific version is `cos-nodejs-sdk-v5`.

The COS SDK can be referenced and used within the code as follows:
```
var COS = require('cos-nodejs-sdk-v5');
```
For more information on how to use the COS SDK, please see [COS SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/8629).

### Built-in library in environment

- The following libraries are supported in Node.js 12.16 runtime:
<table><thead>
<tr><th width="60%">Library Name</th><th width="40%">Version</th></tr>
</thead>
<tbody><tr>
<td align="left">cos-nodejs-sdk-v5</td>
<td align="left">2.5.20</td>
</tr>
<tr>
<td align="left">base64-js</td>
<td align="left">1.3.1</td>
</tr>
<tr>
<td align="left">buffer</td>
<td align="left">5.5.0</td>
</tr>
<tr>
<td align="left">crypto-browserify</td>
<td align="left">3.12.0</td>
</tr>
<tr>
<td align="left">ieee754</td>
<td align="left">1.1.13</td>
</tr>
<tr>
<td align="left">imagemagick</td>
<td align="left">0.1.3</td>
</tr>
<tr>
<td align="left">isarray</td>
<td align="left">2.0.5</td>
</tr>
<tr>
<td align="left">jmespath</td>
<td align="left">0.15.0</td>
</tr>
<tr>
<td align="left">lodash</td>
<td align="left">4.17.15</td>
</tr>
<tr>
<td align="left">microtime</td>
<td align="left">3.0.0</td>
</tr>
<tr>
<td align="left">npm</td>
<td align="left">6.13.4</td>
</tr>
<tr>
<td align="left">punycode</td>
<td align="left">2.1.1</td>
</tr>
<tr>
<td align="left">puppeteer</td>
<td align="left">2.1.1</td>
</tr>
<tr>
<td align="left">qcloudapi-sdk</td>
<td align="left">0.2.1</td>
</tr>
<tr>
<td align="left">querystring</td>
<td align="left">0.2.0</td>
</tr>
<tr>
<td align="left">request</td>
<td align="left">2.88.2</td>
</tr>
<tr>
<td align="left">sax</td>
<td align="left">1.2.4</td>
</tr>
<tr>
<td align="left">scf-nodejs-serverlessdb-sdk</td>
<td align="left">1.1.0</td>
</tr>
<tr>
<td align="left">tencentcloud-sdk-nodejs</td>
<td align="left">3.0.147</td>
</tr>
<tr>
<td align="left">url</td>
<td align="left">0.11.0</td>
</tr>
<tr>
<td align="left">uuid</td>
<td align="left">7.0.3</td>
</tr>
<tr>
<td align="left">xml2js</td>
<td align="left">0.4.23</td>
</tr>
<tr>
<td align="left">xmlbuilder</td>
<td align="left">15.1.0</td>
</tr>
</tbody></table>

- The following libraries are supported in Node.js 10.15 runtime:
<table>
<thead>
<tr><th width="60%">Library Name</th><th width="40%">Version</th></tr>
</thead>
<tbody><tr>
<td align="left">cos-nodejs-sdk-v5</td>
<td align="left">2.5.14</td>
</tr>
<tr>
<td align="left">base64-js</td>
<td align="left">1.3.1</td>
</tr>
<tr>
<td align="left">buffer</td>
<td align="left">5.4.3</td>
</tr>
<tr>
<td align="left">crypto-browserify</td>
<td align="left">3.12.0</td>
</tr>
<tr>
<td align="left">ieee754</td>
<td align="left">1.1.13</td>
</tr>
<tr>
<td align="left">imagemagick</td>
<td align="left">0.1.3</td>
</tr>
<tr>
<td align="left">isarray</td>
<td align="left">2.0.5</td>
</tr>
<tr>
<td align="left">jmespath</td>
<td align="left">0.15.0</td>
</tr>
<tr>
<td align="left">lodash</td>
<td align="left">4.17.15</td>
</tr>
<tr>
<td align="left">microtime</td>
<td align="left">3.0.0</td>
</tr>
<tr>
<td align="left">npm</td>
<td align="left">6.4.1</td>
</tr>
<tr>
<td align="left">punycode</td>
<td align="left">2.1.1</td>
</tr>
<tr>
<td align="left">puppeteer</td>
<td align="left">2.0.0</td>
</tr>
<tr>
<td align="left">qcloudapi-sdk</td>
<td align="left">0.2.1</td>
</tr>
<tr>
<td align="left">querystring</td>
<td align="left">0.2.0</td>
</tr>
<tr>
<td align="left">request</td>
<td align="left">2.88.0</td>
</tr>
<tr>
<td align="left">sax</td>
<td align="left">1.2.4</td>
</tr>
<tr>
<td align="left">scf-nodejs-serverlessdb-sdk</td>
<td align="left">1.0.1</td>
</tr>
<tr>
<td align="left">tencentcloud-sdk-nodejs</td>
<td align="left">3.0.104</td>
</tr>
<tr>
<td align="left">url</td>
<td align="left">0.11.0</td>
</tr>
<tr>
<td align="left">uuid</td>
<td align="left">3.3.3</td>
</tr>
<tr>
<td align="left">xml2js</td>
<td align="left">0.4.22</td>
</tr>
<tr>
<td align="left">xmlbuilder</td>
<td align="left">13.0.2</td>
</tr>
</tbody></table>

- The following libraries are supported in the Node.js 8.9 runtime:
<table>
<thead>
<tr><th width="60%">Library Name</th><th width="40%">Version</th></tr>
</thead>
<tbody><tr>
<td align="left">cos-nodejs-sdk-v5</td>
<td align="left">2.5.8</td>
</tr>
<tr>
<td align="left">base64-js</td>
<td align="left">1.2.1</td>
</tr>
<tr>
<td align="left">buffer</td>
<td align="left">5.0.7</td>
</tr>
<tr>
<td align="left">crypto-browserify</td>
<td align="left">3.11.1</td>
</tr>
<tr>
<td align="left">ieee754</td>
<td align="left">1.1.8</td>
</tr>
<tr>
<td align="left">imagemagick</td>
<td align="left">0.1.3</td>
</tr>
<tr>
<td align="left">isarray</td>
<td align="left">2.0.2</td>
</tr>
<tr>
<td align="left">jmespath</td>
<td align="left">0.15.0</td>
</tr>
<tr>
<td align="left">lodash</td>
<td align="left">4.17.4</td>
</tr>
<tr>
<td align="left">npm</td>
<td align="left">5.6.0</td>
</tr>
<tr>
<td align="left">punycode</td>
<td align="left">2.1.0</td>
</tr>
<tr>
<td align="left">puppeteer</td>
<td align="left">1.14.0</td>
</tr>
<tr>
<td align="left">qcloudapi-sdk</td>
<td align="left">0.1.5</td>
</tr>
<tr>
<td align="left">querystring</td>
<td align="left">0.2.0</td>
</tr>
<tr>
<td align="left">request</td>
<td align="left">2.87.0</td>
</tr>
<tr>
<td align="left">sax</td>
<td align="left">1.2.4</td>
</tr>
<tr>
<td align="left">tencentcloud-sdk-nodejs</td>
<td align="left">3.0.56</td>
</tr>
<tr>
<td align="left">url</td>
<td align="left">0.11.0</td>
</tr>
<tr>
<td align="left">uuid</td>
<td align="left">3.1.0</td>
</tr>
<tr>
<td align="left">xml2js</td>
<td align="left">0.4.17</td>
</tr>
<tr>
<td align="left">xmlbuilder</td>
<td align="left">9.0.1</td>
</tr>
</tbody></table>




- The following libraries are supported in Node.js 6.10 runtime:
<table>
<thead>
<tr><th width="60%">Library Name</th><th width="40%">Version</th></tr>
</thead>
<tbody><tr>
<td align="left">base64-js</td>
<td align="left">1.2.1</td>
</tr>
<tr>
<td align="left">buffer</td>
<td align="left">5.0.7</td>
</tr>
<tr>
<td align="left">cos-nodejs-sdk-v5</td>
<td align="left">2.0.7</td>
</tr>
<tr>
<td align="left">crypto-browserify</td>
<td align="left">3.11.1</td>
</tr>
<tr>
<td align="left">ieee754</td>
<td align="left">1.1.8</td>
</tr>
<tr>
<td align="left">imagemagick</td>
<td align="left">0.1.3</td>
</tr>
<tr>
<td align="left">isarray</td>
<td align="left">2.0.2</td>
</tr>
<tr>
<td align="left">jmespath</td>
<td align="left">0.15.0</td>
</tr>
<tr>
<td align="left">lodash</td>
<td align="left">4.17.4</td>
</tr>
<tr>
<td align="left">npm</td>
<td align="left">3.10.10</td>
</tr>
<tr>
<td align="left">punycode</td>
<td align="left">2.1.0</td>
</tr>
<tr>
<td align="left">qcloudapi-sdk</td>
<td align="left">0.1.5</td>
</tr>
<tr>
<td align="left">querystring</td>
<td align="left">0.2.0</td>
</tr>
<tr>
<td align="left">request</td>
<td align="left">2.87.0</td>
</tr>
<tr>
<td align="left">sax</td>
<td align="left">1.2.4</td>
</tr>
<tr>
<td align="left">tencentcloud-sdk-nodejs</td>
<td align="left">3.0.10</td>
</tr>
<tr>
<td align="left">url</td>
<td align="left">0.11.0</td>
</tr>
<tr>
<td align="left">uuid</td>
<td align="left">3.1.0</td>
</tr>
<tr>
<td align="left">xml2js</td>
<td align="left">0.4.17</td>
</tr>
<tr>
<td align="left">xmlbuilder</td>
<td align="left">9.0.1</td>
</tr>
</tbody></table>




## Relevant Operations
For more information on how to use relevant features, please see the following documents:
- [Network Configuration Management](https://intl.cloud.tencent.com/document/product/583/38377)
- [Role and Authorization](https://intl.cloud.tencent.com/document/product/583/38176)
