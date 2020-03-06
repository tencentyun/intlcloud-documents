When writing code in a language supported by the SCF platform, you need to adopt a common paradigm that includes the following core concepts:

## Execution Method 
The execution method determines where the SCF platform starts to execute your code, and is specified in the form of `filename.method name`. When SCF calls a function, it will start executing your code by looking for the execution method. For example, if the user-specified execution method is `index.handler`, the platform will first look for the index file in the code package and find the handler method in the file to start execution.

You must follow the platform-specific programming model when writing the execution method, which specifies fixed input parameters: event data "event" and environment data "context". The execution method should handle the parameters and can call any other method in the code arbitrarily.

## Function Input Parameters

Function input parameters refer to the content that is passed to the function when the function is triggered. Usually, there are two input parameters: event and context. Depending on the programming language and environment, the number of input parameters may vary. For the specific differences in terms of input parameters for different languages, see [Notes on Programming Languages](https://intl.cloud.tencent.com/document/product/583/11061).
> **Note:**
> To ensure uniformity for each programming language and environment, `event` and `context`are uniformly encapsulated using the JSON data format.

### event Input Parameter
SCF passes the `event` input parameter to the execution method, through which the code will interact with the event that triggers the function.
For example, if a file upload action triggers the function, the code can get all the information of the file from the event parameter, including the file name, download path, file type, and size.
Different triggers pass different data structures when triggering functions. The specific data structures can be seen in [Function Trigger Description](https://cloud.tencent.com/document/product/583/9705). In addition, if the function is triggered by TencentCloud API, you can customize the input parameters passed to the function.

### context Input Parameter 
SCF passes the `context` input parameter to the execution method, through which the code can get to know the runtime environment and related content of the current request. The current context is as follows:
```
{
    "time_limit_in_ms": 3000, 
    "request_id": "627466b4-8049-11e8-8758-5254005d5fdb",
    "memory_limit_in_mb": 512
}
```
This contains the execution timeout of the current call, the memory limit, and the current request ID.

> **Note:**
> The content of the context structure will likely be increased as the SCF platform is iterated.

## Function Return
The return value after the function is executed will be obtained by the SCF platform and handled according to different triggers.

* Sync triggering: For a function triggered synchronously, the request will not return during function execution. After the function is executed, the return value will be encapsulated into JSON format and returned to the caller. If triggered by API Gateway or the RequestResponse method in TencentCloud API, the function is triggered synchronously.
* Async triggering: For a function that is triggered asynchronously, the trigger request will return after the triggering event is received by the SCF platform. After the function is executed, the return value will be encapsulated into JSON format and stored in the log. If you need to obtain the return value of the function after async triggering, you can record the requestId in the request return, and after the function is executed, query the log using the requestId to get the return value of this function execution.

> **Note:**
> To ensure uniformity for each programming language and environment, the function return is uniformly encapsulated using the JSON data format.

## Log
The SCF platform stores all the records of function calls and the outputs of the function code in the log. You can use the printout or log statement in the programming language to generate the output log for debugging and troubleshooting.

The function execution log contains function name, start time, execution duration, billable duration, actual memory usage, return code, return value, code log, and execution status information.

It usually has the following data structures:
```
{
    "functionName": "testnode",
    "retMsg": "\"ok\"",
    "requestId": "b33b9d0b-9c51-11e7-b38f-525400c7c826",
    "startTime": "2017-09-18 17:13:57",
    "retCode": 0,
    "invokeFinished": 1,
    "duration": 7.437,
    "billDuration": 100,
    "memUsage": 131072,
    "log": "2017-09-18T09:13:57.155Z\tundefined\tHello World\n2017-09-18T09:13:57.156Z\tundefined\t{ Records: [ { CMQ: [Object] } ] }\n2017-09-18T09:13:57.158Z\tundefined\t{ msgBody: '3',\n  msgId: '3096224743817223',\n  msgTag: '',\n  publishTime: '2017-09-18T17:13:57Z',\n  requestId: '5761047512720426853',\n  subscriptionName: 'test',\n  topicName: 'test',\n  topicOwner: 1251762227,\n  type: 'topic' }\n2017-09-18T09:13:57.159Z\tundefined\t{ callbackWaitsForEmptyEventLoop: [Getter/Setter],\n  done: [Function: done],\n  succeed: [Function: succeed],\n  fail: [Function: fail],\n  memory_limit_in_mb: 128,\n  time_limit_in_ms: 30000 }\n"
}
```

## Considerations
Due to the nature of SCF, you **must** write your function code in a stateless style. State features in the lifecycle of a function such as local file storage will be destroyed after the function call ends. Therefore, it is recommended to store persistent states in CDB, COS, Cloud Memcached, or other cloud storage services.
