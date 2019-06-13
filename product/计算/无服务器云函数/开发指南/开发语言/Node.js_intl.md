Currently, the following versions of Node.js programming language are supported:

* Node.js 6.10
* Node.js 8.9

## Function Form

The Node.js function form is generally as follows:

```
exports.main_handler = (event, context, callback) => {
    console.log("Hello World")
    console.log(event)
    console.log(context)
    callback(null, event); 
};
```

## Execution Method

When you create an SCF function, you need to specify an execution method. If the Node.js programming language is used, the execution method is similar to `index.main_handler`, where `index` indicates that the executed entry file is `index.js`, and `main_handler` indicates that the executed entry function is `main_handler`. When submitting the zip code package by uploading the zip file locally or through COS, please make sure that the root directory of the package contains the specified entry file, the file contains the entry function specified by the definition, and the names of the file and function match those entered in the trigger; otherwise, execution will fail as the entry file or entry function cannot be found.

## Input Parameters

The input parameters in the Node.js environment include event, context, and callback, where callback is optional.

* event: This parameter is used to pass the trigger event data.
* context: This parameter is used to pass runtime information to your handler.
* callback: This parameter is used to return the desired information to the caller. If there is no such parameter value, the return value will be null.

## Return and Exception

Your handler needs to use the `callback` input parameter to return information. The syntax of `callback` is:

```
callback(Error error, Object result);
```

Where:

* error: This is an optional parameter, which is used to return the error content when function execution fails internally. It can be set to null in case of success.
* result: This is an optional parameter, which is used to return the successful execution result information of the function. The parameters need to be compatible with JSON.stringify for serialization to JSON format.

If callback is not called in the code, the SCF backend will make the call implicitly and return null.

The return value will be handled differently depending on the type of call when the function is called. The return value of a sync call will be serialized to JSON format and then returned to the caller, while the return value of an async call will be discarded. In addition, the return value will be displayed at the `ret_msg` position in the function log for both sync call and async call.

## Node.js Event Loop

As Node.js uses a lot of async event loops to handle callbacks, async events are also supported when executing Node.js code in SCF. After the callback is called in the entry function, the SCF backend will wait until the event queue gets empty before returning.

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

As you can see, the async task set by setTimeout is executed after the callback is executed, and the function does not actually return until the async task is completed.


### Turn off event loop wait

Some externally referenced libraries may cause the event loop to never get empty. In this case, the function will be unable to return until it times out. In order to avoid the impact of external libraries, we can control the function return timing by turning off event loop wait. In the following two ways, we can modify the default callback behavior to avoid waiting for the event loop to get empty.

* Set context.callbackWaitsForEmptyEventLoop to false
* Call back using context.done

By setting `context.callbackWaitsForEmptyEventLoop = false;` before the `callback` command is executed, the SCF backend can freeze the process immediately after the callback command is called, and return immediately after the synchronization command is completed without waiting for the event in the event loop.

You can also replace the `callback` command with the context.done callback. The input parameters of the context.done callback are the same as those of the callback command. The context.done callback will also freeze the process of the event loop listener after it is executed, and return immediately after the synchronization command is executed.

## Log

You can use the following statements in the program to output the log:

* console.log()
* console.error()
* console.warn()
* console.info()

The output can be viewed at the `log` location in the function log.

## Included Library and Usage

### COS SDK

SCF's runtime environment already contains the [COS SDK for Node.js](https://cloud.tencent.com/document/product/436/8629), and the specific version is `cos-nodejs-sdk-v5`.

The COS SDK can be referenced and used within the code as follows:


```
var COS = require('cos-nodejs-sdk-v5');
```

For more detailed instructions on how to use the COS SDK, see [COS SDK for Node.js](https://cloud.tencent.com/document/product/436/8629).
