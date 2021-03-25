When writing code in a language supported by the SCF platform, you need to adopt a common paradigm that includes the following core concepts:
## Execution Method
When the SCF platform invokes a function, it will first find an execution method as the entry point to execute your code. At this time, you need to set in the format of **filename.execution method name**.
For example, if the user-configured execution method is `index.handler`, the SCF platform will first look for the `index` file in the code package and find the `handler` method in the file to start execution.
You must follow the platform-specific programming model when writing the execution method as shown below:
```
def method_name(event,context): 
    ...
    return some_value
```
This model specifies the fixed `event` data and `context` data as input parameters. In the execution method, you should handle the parameters and can call any other method in the code arbitrarily.

## Function Input Parameters

Function input parameters refer to the content that is passed to the function when the function is triggered. Usually, there are two input parameters: `event` and `context`. However, the number of input parameters may vary by programming language and environment. For more information, please see [Python](https://intl.cloud.tencent.com/document/product/583/11061).

#### event input parameter
#### Usage
 The parameter type is `dict`. The `event` input parameter is passed to the execution method, through which the code will interact with the event that triggers the function. For example, if a file upload operation triggers the function, the code can get all the information of the file from the `event` parameter, including the filename, download path, file type, and size.
#### Instructions
The value of `event` varies by function:
- If the function is triggered by a Tencent Cloud service, the service will pass the event to SCF as the `event` parameter in a platform-predefined unchangeable format. You can write code based on this format and get information from the `event` parameter. For example, when COS triggers a function, the specific information of the bucket and the file will be passed to the `event` parameter in <a href="https://intl.cloud.tencent.com/document/product/583/9707">JSON</a> format.
- If the function is invoked by another application, you can freely define a parameter of <code>dict</code> type between the invoker and the function code, where the invoker passes in the data in the format agreed upon, and the function code gets the data in the format.<br>For example, you can define a data structure <code>{"key":"XXX"}</code> of <code>dict</code> type, and when the invoker passes in the data <code>{"key":"abctest"}</code>, the function code can get the value <code>abctest</code> through <code>event[key]</code>.

#### context input parameter
#### Usage
The `context` input parameter is passed to the execution method, through which the code can get to know the runtime environment and related content of the current request.
#### Instructions
Please see the `context` input parameter below for specific information:
```
{
		getRemainingTimeInMillis: [Function: getRemainingTimeInMillis],
		memory_limit_in_mb: 128,
		time_limit_in_ms: 3000,
		request_id: '4ca7089c-3bb0-48cf-bcdb-26d130fed2ae',
		environment: '{"SCF_NAMESPACE":"default"}',
		environ: 'SCF_NAMESPACE=default;SCF_NAMESPACE=default',
		function_version: '$LATEST',
		function_name: 'test',
		namespace: 'default',
		tencentcloud_region: 'ap-chengdu',
		tencentcloud_appid: '1253970226',
		tencentcloud_uin: '3473058547' 
}
```
This contains the execution timeout of the current invocation, the memory limit, and the current request ID.

>! The content of the context structure may be increased as the SCF platform is iterated.


<br>
After understanding the basic usage of `event` and `context` input parameters, you should pay attention to the following points when writing function code:
<ul>
	<li>To ensure uniformity for each programming language and environment, `event` and `context` should be uniformly encapsulated in the JSON data format.</li>
	<li>Different triggers pass different data structures when triggering functions. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/583/9705">Trigger Overview</a>.</li>
	<li>If the function is triggered by TencentCloud API, you can customize the input parameters passed to the function.</li>
		<li>If the function does not need any input, you can ignore the `event` and `context` parameters in your code.</li>
	</ul>


## Function Return
The SCF platform will get the returned value after the function is executed and handle according to different trigger type as listed below.
<table>
	<tr>
	<th>Trigger Type</th>
	<th>Handling Method</th>
	</tr>
	<tr>
	<td>Sync triggering</td>
	<td>
		<ul class="params">
		<li>If triggered by API Gateway or the `RequestResponse` method in TencentCloud API, the function is triggered synchronously.</li>
		<li>For a function triggered synchronously, the SCF platform will not return the triggering request during function execution.</li>
		<li>After the function is executed, the SCF platform will encapsulate the returned value into JSON format and return it to the invoker.</li>
		</ul>
	</td>
	</tr>
	<tr>
	<td>Async triggering</td>
	<td>
		<ul class="params">
			<li>For a function that is triggered asynchronously, the SCF will return the triggering request after receiving the triggering event.</li>
			<li>After the function is executed, the returned value will be encapsulated into JSON format and stored in the log.</li>
			<li>After the function execution is completed, you can query the log by recording `requestId` in the request return to get the returned value of the asynchronously triggered function.</li>
		</ul>
	</td>
	</tr>
</table>

When the code in a function returns a specific value, it usually returns a specific data structure; for example:

<table>
<tr>
<th>Runtime Environment</th>
<th>Returned Structure Type</th>
</tr>
<tr>
<td>Python</td>
<td>Simple or <code>dict</code> data structure</td>
</tr>
<tr>
<td>Node.js</td>
<td> <code>JSON Object</code></td>
</tr>
<tr>
<td>PHP</td>
<td><code>Array</code> structure</td>
</tr>
<tr>
<td>Go</td>
<td>Simple data structure or <code>struct</code> with JSON description</td>
</tr>
</table>


To ensure uniformity for different programming languages and environments, the function return will be uniformly encapsulated in the JSON data format. For example, after SCF gets the returned value of the function in the above runtime environment, it will convert the returned data structure to JSON and return it to the invoker.
>!
>- You should ensure that the returned value of the function can be converted to JSON format. If the object is returned directly and there is no JSON conversion method, SCF will fail when executing JSON conversion and prompt an error.
>- For example, the returned value in the above runtime environment does not need to be converted to JSON format before it is returned; otherwise, the output string will be converted again.


## Exception Handling
If an exception occurs during testing and executing a function, the SCF platform will handle the exception as much as possible and write the exception information into the log. Exceptions generated by function execution include caught exceptions (handled errors) and uncaught exceptions (unhandled errors).

### Handling method
This document provides the following three ways to throw exceptions, and you can choose how to handle exceptions in the code based on your actual needs.
>?You can log in to the [SCF Console](https://console.cloud.tencent.com/scf/index) and follow the steps below to test exception handling:
>1. Create a function and copy the following function code without adding any triggers.
>2. Click **Test** in the console and select the "Hello World" test sample for testing.

#### Throw exceptions explicitly
- **Sample**
```
def always_failed_handler(event,context):
    raise Exception('I failed!')
```
- **Description**
This function will throw an exception during execution and return the following error message. The SCF platform will record this error message in the function log.
```
File "/var/user/index.py", line 2, in always_failed_handler
raise Exception('I failed!')
Exception: I failed!
```

#### Inherit the `Exception` class
- **Sample**
```
class UserNameAlreadyExistsException(Exception): pass
def create_user(event):
    raise UserNameAlreadyExistsException('
		The username already exists,
		please change a name!')
```
- **Description**
You can define how to handle errors in your code to ensure the robustness and scalability of your application.

#### Use the `Try` statement to catch errors
- **Sample**
```
def create_user(event):
    try:
        createUser(event[username],event[pwd])
    except UserNameAlreadyExistsException,e:
        //catch error and do something
```
- **Description**
You can define how to handle errors in your code to ensure the robustness and scalability of your application.


### Returned error message
If exception handling and error capture are not performed in your code logic, the SCF platform will capture errors as much as possible such as when your function suddenly crashes and exits during execution. The platform will return a general error message if it cannot capture an error that occurs.
The table below lists some common errors in code execution:

| Error Scenario | Error Message |
| ------------------- | ------------------------------------------------------------ |
| `raise` is used to throw an exception | {File "/var/user/index.py", line 2, in always_failed_handler raise Exception('xxx') Exception: xxx} |
| The handler does not exist      | {'module' object has no attribute 'xxx'}                     |
| The dependent module does not exist    | {global name 'xxx' is not defined}                           |
| Timed out                | {"time out"}                                                 |

## Log
The SCF platform stores all the records of function invocations and the outputs of the function code in logs. You can use the printout or log statement in the programming language to generate the output logs for debugging and troubleshooting.

### Log composition
A function execution log contains function name, start time, execution duration, billable duration, actual memory usage, return code, returned value, code log, and execution status.

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

### Log write
The log statement provides the function with the necessary information in the execution process, which is necessary for developers to troubleshoot code issues. The SCF platform writes all the logs generated by the log statement in your code to the logging system. If you use the console to invoke the function, the console will display the same logs.

You can generate logs through the `print` statement or the `Logger` function in the logging module as shown below:

#### Use the `logging` statement
The following sample code uses the logging module to write information into the log:
```
import logging
logger = logging.getLogger()
def my_logging_handler(event):
    logger.info('got event{}'.format(event))
    logger.error('something went wrong')
    return 'Hello World!'
```
You can go to the logs tab in the console or use the <a href="https://intl.cloud.tencent.com/document/product/583/18583">GetFunctionLogs</a> API to view the log information in the code.

>? The log level identifies the log type, such as <code>INFO</code>, <code>ERROR</code>, and <code>DEBUG</code>.

#### Use the `print` statement
Use the `print` statement in the code:
```
def print_handler(event):
    print('this will show up in logging')
    return 'Hello World!'
```

>! When you invoke this function synchronously by using the **Test** button in the console, the console will display the `print` statement and `return` value.



### Getting log
You can get a function execution log in the following methods:

<table>
	<tr>
	<th>Means</th>
	<th>Method</th>
	</tr>
	<tr>
	<td>SCL CLI</td>
	<td>Run the <code>scf logs</code> command.</td>
	</tr>
	<tr>
	<td>SCF Console</td>
	<td>On the function code page, click <b>Test</b> to synchronously invoke the function. After the execution is completed, the log of this invocation will be displayed directly in the console.</td>
	</tr>
	<tr>
	<td>Trigger invocation</td>
	<td>The logs tab of the function will display the logs generated by every function invocation.</td>
	</tr>
	<tr>
	<td>SCF API</td>
	<td>Use the `GetFunctionLogs` API to get function logs.</td>
	</tr>
	<tr>
	<td>Sync invocation through the `Invoke` API</td>
	<td>The log of this invocation can be obtained in the `logMsg` field of the returned value.</td>
	</tr>
</table>


## Notes
Because of the nature of SCF, you must write your function code in a **stateless** style. State characteristics in the lifecycle of a function such as local file storage will be destroyed after the function invocation ends.
Therefore, you are recommended to store persistent states in TDSQL, COS, TencentDB for Memcached, or other cloud storage services.

## Development Process
For more information on the function development process, please see [Getting Started](https://intl.cloud.tencent.com/document/product/583/9179).


<ul><li>test1</li><li>test2</li></ul>

<ol><li>test3</li><li>test4</li></ol>

<style>
	.params{
		margin-bottom:0px !important;
	}
</style>

