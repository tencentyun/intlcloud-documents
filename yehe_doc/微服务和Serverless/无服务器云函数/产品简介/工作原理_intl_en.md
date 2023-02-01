
## Instance Model of Function Runtime

SCF will execute a function for you when the function receives a triggering request. Instance is the resource for SCF to execute the request. SCF will allocate resources based on the function configuration information (such as memory size) and launch one or multiple instances to process the function request. The SCF platform is responsible for the creation, management, and deletion of all function runtime instances, and you have no permissions to manage them.

The lifecycle of an instance is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0c2ad14f8d31b75b7adbe150b3154037.png)

#### Starting instance 

- If there is no running instance when a request arrives, the request will trigger the startup of an instance. Instance startup usually takes some time, which adds extra time to the invocation that triggers the instance startup. Generally, instance startup is triggered only when a function is invoked for the first time, updated, or invoked again after a long period of inactivity.
- The instance startup time will be reflected in the `Coldstart` field in the `Init Report` or `Provisioned Report` line of the function execution log.
- You can use the [provisioned concurrency](https://intl.cloud.tencent.com/document/product/583/37704) feature to start instances in advance to avoid triggering the instance startup when the function request arrives.
- The instance startup time is limited by the function's [initialization timeout period](https://intl.cloud.tencent.com/document/product/583/19805). If the former is longer than the latter, instance startup will fail. You can accelerate instance startup or increase the initialization timeout period accordingly as detailed below.

Method to accelerate the three phases of instance startup:

- **Code preparation**: The platform pulls the function code, layer, or image uploaded by you to prepare for function execution. The code preparation time is positively proportional to the sizes of code package, layer, and image. We recommend you reduce the code package size as much as possible and only keep the code files and dependencies necessary for function execution in order to minimize the code preparation time. This time will be reflected in the `PullCode` field in the `Init Report` or `Provisioned Report` line of the function execution log.
- **Runtime initialization**: The platform prepares the runtime environment that function execution depends on according to your function configuration. This time will be reflected in the `InitRuntime` field in the `Init Report` or `Provisioned Report` line of the function execution log.
- **Function code initialization**: The code initialization time is positively proportional to the complexity of the code logic. We recommend you optimize the code logic as much as possible to minimize the code initialization time. This time will be reflected in the `InitFunction` field in the `Init Report` or `Provisioned Report` line of the function execution log.
  - Code deployment-based event-triggered function: The code logic before the [execution method](https://intl.cloud.tencent.com/document/product/583/19805) configured for the function will be executed during instance startup. For example, if the entry function is `main_handler`, all the code logic before `main_handler` will be executed.
  - Code deployment-based HTTP-triggered function: The bootstrap file `scf_bootstrap` and the code logic before listening port 9000 will be executed during instance startup.
  - Image deployment-based function: For event-triggered functions, the code logic before the [execution method](https://intl.cloud.tencent.com/document/product/583/19805) configured for the function will be executed; for HTTP-triggered functions, the code logic before the bootstrap file `scf_bootstrap` and listening port 9000 will be executed.

#### Reusing instance
In order to minimize the additional time caused by instance startup, the platform will try to reuse the instance for subsequent invocations. After the instance processes the function request, it will be stored for a period of time according to the actual situation of the platform for next invocations and will be used first during this period.

The meaning of instance reuse is as follows:

- All declarations outside the [execution method](https://intl.cloud.tencent.com/document/product/583/9210) part in your code remain initialized and can be reused directly when the function is invoked again. For example, if a database connection is established in your function code, the original connection can be used directly when the container is reused. You can add logic to your code to check whether a connection already exists before creating a new one.
- Each container provides some disk space in the `/tmp` directory. The contents of this directory are retained when the container is retained, providing a temporary cache that can be used for multiple invocations. It is possible to use the contents of the disk directly when the function is invoked again. You can add extra code to check whether such data is in the cache.

>! Do not assume that the instance is always reused in the function code, because reuse is related to the single actual invocation, and it cannot be guaranteed whether a new instance will be created or an existing one will be reused.

#### Repossessing instance
The platform will repossess instances that have not processed requests for a certain period of time.



## Temporary Disk Space

Each function has a temporary disk space of 512 MB (`/tmp`) during execution. You can perform certain read and write operations on the space in the execution code or create subdirectories, but this part of data may **not** be retained after function execution is completed. Therefore, if you need to persistently store the data generated during execution, use [COS](https://www.tencentcloud.com/document/product/436) or external persistent storage services such as Redis/Memcached.

## Call Types

The SCF platform supports both sync and async calls of functions.

#### Sync invocation

 Sync invocation will wait for the execution result of the function after the invocation request is sent.

#### Async invocation[](id:asynchronous)

- Async call will only send the request and get the request ID of the current request, but not wait for the result.
- When an async invocation occurs, the async event will be placed in the async queue built in SCF and then consumed by the event execution function in the async queue. Async queues have the following restrictions:
 - Async queues are at the trigger level, and one function trigger has one queue.
 - An async event can be retained in a queue for up to 6 hours.
 - There can be up to 100,000 messages in an async queue.
- The retry policy may vary by async queue. For more information, see [Retry Policy](https://intl.cloud.tencent.com/document/product/583/39851).


#### Defining function invocation type

The call type is independent of the configuration of the function itself and can only be controlled when the function is called.

In the following call scenarios, you can freely define the call type of the function:

- The SCF function is invoked by a written application. If you need to make a sync invocation, use the [InvokeFunction](https://intl.cloud.tencent.com/document/product/583/41408) API; if you need to make an async invocation, use the [Invoke](https://intl.cloud.tencent.com/document/product/583/17243) API and pass in the `invokeType=Event` parameter.
- The SCF function is manually invoked (with API or CLI) for testing. The parameters for the invocation are the same as above.

If you use another Tencent Cloud service as the event source, the invocation type of the cloud service is predefined.

- Sync invocation: By [API Gateway trigger](https://intl.cloud.tencent.com/document/product/583/12513), [CLB trigger](https://intl.cloud.tencent.com/document/product/583/39849), and [CKafka trigger](https://intl.cloud.tencent.com/document/product/583/17530), for example.
- Async invocation: By [COS trigger](https://intl.cloud.tencent.com/document/product/583/9707), [timer trigger](https://intl.cloud.tencent.com/document/product/583/9708), and [CMQ topic trigger](https://intl.cloud.tencent.com/document/product/583/9705), for example. For more information, see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).


## Usage Restrictions

For the restrictions on function usage quotas and related environments, see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637).

### Function concurrency

The function concurrency is the number of executions of the function code in any given period of time. For the current SCF function, the request is executed once each time an event is published. Therefore, the number of events (i.e., requests) published by the trigger affects the function concurrency. You can use the formula below to estimate the total number of concurrent function instances.

```
Requests per second * function execution duration (in seconds) 
```

For example, for a function that handles COS events, if the function takes an average of 0.2 seconds (i.e., 200 milliseconds) for execution and COS publishes 300 requests per second to the function, then 300 \* 0.2 = 60 function instances will be generated simultaneously.


### Concurrency limits

Currently, SCF has a limit on the amount of concurrency for each function. You can view the limit for the current function in [Concurrency Overview](https://intl.cloud.tencent.com/document/product/583/37040).
If an invocation causes the function concurrency to exceed the default limit, the invocation will be blocked and not executed by SCF. Restricted invocations are handled differently depending on the function invocation type:

- Sync invocation: If the function is restricted when invoked synchronously, a [432 error](https://intl.cloud.tencent.com/document/product/583/35311) will be returned directly.
- Async invocation: If the function is restricted when invoked asynchronously, SCF will [retry](https://intl.cloud.tencent.com/document/product/583/39851) the restricted event according to a certain policy.

## Execution Environment and Available Libraries

The current SCF execution environment is built based on the following:
- Standard CentOS 7.2

If you need to include executable binaries, dynamic libraries, or static libraries in your code, make sure that they are compatible with this execution environment.
Based on different language environments, there are base libraries and additional libraries installed for the corresponding language in the SCF execution environment. You can view the additional libraries installed in the environment in the descriptions of each language:
- [Python](https://intl.cloud.tencent.com/document/product/583/40323)
- [Node.js](https://intl.cloud.tencent.com/document/product/583/11060)
- [Golang](https://intl.cloud.tencent.com/document/product/583/18032)
- [PHP](https://intl.cloud.tencent.com/document/product/583/17531)
- [Java](https://intl.cloud.tencent.com/document/product/583/12214)


## Deployment Mode
Serverless Cloud Function (SCF) provides two deployment methods of code deployment and image deployment and supports two function types of event-triggered function and HTTP-triggered function. Different deployment methods and function types require different specifications during code development. This document describes the writing specifications and related concepts of event-triggered function in code deployment. For more information on [image deployment](https://intl.cloud.tencent.com/document/product/583/41076) and [HTTP-triggered function](https://intl.cloud.tencent.com/document/product/583/40688), see the corresponding documents.


### SCF event-triggered function
An SCF event-triggered function involves three basic concepts: execution method, function input parameter, and function return.
The above concepts correspond respectively to the following in general project development:
- **Execution method**: Corresponds to the main function of the project and is the starting point of program execution.
- **Function input parameter**: Refers to function input parameters in a normal sense. However, in the SCF environment, the input parameters of an entry function are fixed values. For more information, see [Function Input Parameters](#input).
- **Function return**: Corresponds to the returned value of the main function in the project. After the function returns, the code execution ends.




#### Execution method

When the SCF platform invokes a function, it will first find an execution method as the entry point to execute your code. At this time, you need to set in the format of **filename.execution method name**.
For example, if the user-configured execution method is `index.handler`, the SCF platform will first look for the `index` file in the code package and find the `handler` method in the file to start execution.
In the execution method, you can process the input parameters of the entry function and call other methods in the code arbitrarily. In SCF, the completion of the execution of the entry function or the exception of the execution of the function marks the end of execution.


#### Function input parameters[](id:input)

Function input parameters refer to the content that is passed to the function when the function is triggered. Usually, there are two input parameters: `event` and `context`. However, the number of input parameters may vary by programming language and environment. For more information, see [Code Development](https://www.tencentcloud.com/document/product/583/40190).
<dx-tabs>
::: event

#### Usage

The `event` parameter is of `dict` type and contains the basic information that triggers the function. It can be in a platform-defined or custom format. After the function is triggered, the event can be processed inside the code.

#### Instructions

There are two ways to trigger an SCF function:

1. Trigger by calling [TencentCloud API](https://intl.cloud.tencent.com/document/product/583/17243).
2. Trigger by binding a [trigger](https://intl.cloud.tencent.com/document/product/583/9705).   


These two SCF trigger methods correspond to two event formats:

- **TencentCloud API:**
  You can freely define a parameter of `dict` type between the invoker and the function code, where the invoker passes in the data in the format agreed upon, and the function code gets the data in the format.
 **Sample:**
  You can define a data structure `{"key":"XXX"}` of `dict` type, and when the invoker passes in the data `{"key":"abctest"}`, the function code can get the value `abctest` through `event [key]`.


- **Trigger:**
  SCF can be connected with various Tencent Cloud services such as API Gateway, COS, and CKafka, so you can bind a corresponding Tencent Cloud service trigger to a function. When the function is triggered, the service will pass the event to SCF as the `event` parameter in a platform-predefined unchangeable format. You can write code based on this format and get information from the `event` parameter.
 **Sample:**
  When COS triggers a function, the specific information of the bucket and the file will be passed to the `event` parameter in <a href="https://intl.cloud.tencent.com/document/product/583/9707#cos-.E8.A7.A6.E5.8F.91.E5.99.A8.E7.9A.84.E4.BA.8B.E4.BB.B6.E6.B6.88.E6.81.AF.E7.BB.93.E6.9E.84">JSON</a> format. The processing of the triggering event can be completed by parsing the `event` information in the function code.
  :::
  ::: context

#### Usage

`context` is an input parameter provided by the SCF platform. It is passed to the execution method, by parsing which the code can get the runtime environment and related information of the current request.

#### Instructions

The fields and descriptions of the `context` input parameter provided by SCF are as follows:

<table>
<thead><tr><th align="left">Field</th><th align="left">Description</th></tr></thead>
<tbody>
<tr><td align="left"><code>memory_limit_in_mb</code></td><td align="left">Configured function memory size</td></tr>
<tr><td align="left"><code>time_limit_in_ms</code></td><td align="left">Timeout period for function execution</td></tr>
<tr><td align="left"><code>request_id</code></td><td align="left">Function execution request ID</td></tr>
<tr><td align="left"><code>environment</code></td><td align="left">Function namespace information</td></tr>
<tr><td align="left"><code>environ</code></td><td align="left">Function namespace information</td></tr><tr><td align="left"><code>function_version</code></td><td align="left">Function version information</td></tr>
<tr><td align="left"><code>function_name</code></td><td align="left">Function name</td></tr><tr><td align="left"><code>namespace</code></td><td align="left">Function namespace information</td></tr>
<tr><td align="left"><code>tencentcloud_region</code></td><td align="left">Function region</td></tr>
<tr><td align="left"><code>tencentcloud_appid</code> </td><td align="left">Function's Tencent Cloud APPID</td></tr><tr><td align="left"><code>tencentcloud_uin</code></td><td align="left">Function's Tencent Cloud account ID </td></tr>
</tbody>
</table><dx-alert infotype="notice" title="">
To ensure compatibility, the descriptions of the namespace at different stages of the SCF function are retained in the context.
 The content of the context structure may be increased as the SCF platform is iterated.
</dx-alert>

You can print the context information through the standard output statement in the function code. Take the `python` runtime environment as an example:

``` Python
# -*- coding: utf8 -*-
import json
def main_handler (event, context):
    print (context)
    return ("Hello World")
```

The following context information can be obtained:
<dx-codeblock>
::: json
{"memory_limit_in_mb": 128, "time_limit_in_ms": 3000, "request_id": "f03dc946-3df4-45a0-8e54-xxxxxxxxxxxx", "environment": "{\"SCF_NAMESPACE\":\"default\"}", "environ": "SCF_NAMESPACE=default;SCF_NAMESPACE=default", "function_version": "$LATEST", "function_name": "hello-from-scf", "namespace": "default", "tencentcloud_region": "ap-guangzhou", "tencentcloud_appid": "12xxxxx384", "tencentcloud_uin": "10000xxxxx36"}
:::
</dx-codeblock>

:::

</dx-tabs>


After understanding the basic usage of `event` and `context` input parameters, you should pay attention to the following points when writing function code:

<ul>
	<li >To ensure uniformity for each programming language and environment, `event` and `context` should be uniformly encapsulated in the `JSON` data format.</li>
	<li >Different triggers pass different data structures when triggering functions. For more information, see <a href="https://intl.cloud.tencent.com/document/product/583/9705">Trigger Overview</a>.</li>
		<li >If the function does not need any input, you can ignore the `event` and `context` parameters in your code.</li>
	</ul>


#### Function response

The SCF platform will get the returned value after the function is executed and handle according to different trigger type as listed below.

<table>
	<tr>
	<th > Trigger Type </th>
	<th > Handling Method </th>
	</tr>
	<tr>
	<td > Sync triggering </td>
	<td>
		<ul class="params">
<li > If triggered by API Gateway or the TencentCloud API for sync invocation, the function will be triggered synchronously.</li>
		<li > For a function triggered synchronously, the SCF platform will not return the trigger result during function execution.</li>
		<li > After the function is executed, the SCF platform will encapsulate the returned value into JSON format and return it to the invoker.</li>
		</ul>
	</td>
	</tr>
	<tr>
	<td > Async triggering </td>
	<td>
		<ul class="params">
	<li > For a function that is triggered asynchronously, the SCF will return the triggering request ID after receiving the triggering event.</li>
			<li > After the function is executed, the returned value will be encapsulated into JSON format and stored in the log.</li>
			<li > After the function execution is completed, you can query the log by the request ID in the return to get the returned value of the asynchronously triggered function.</li>
		</ul>
	</td>
	</tr>
</table>


When the code in a function returns a specific value, it usually returns a specific data structure; for example:

<table>
<tr>
<th > Runtime Environment </th>
<th > Returned Structure Type </th>
</tr>
<tr>
<td>Python</td>
<td > Simple or <code>dict</code> data structure</td>
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
<td>GO</td>
<td > Simple data structure or <code>struct</code> with JSON description</td>
</tr>
</table>


To ensure uniformity for different programming languages and environments, the function return will be uniformly encapsulated in the JSON data format. For example, after SCF gets the returned value of the function in the above runtime environment, it will convert the returned data structure to JSON and return it to the invoker.

>!
>
>- You should ensure that the returned value of the function can be converted to JSON format. If the object is returned directly and there is no JSON conversion method, SCF will fail when executing JSON conversion and prompt an error.
>- For example, the returned value in the above runtime environment does not need to be converted to JSON format before it is returned; otherwise, the output string will be converted again.


## Exception Handling

If an exception occurs during testing and executing a function, the SCF platform will handle the exception as much as possible and write the exception information into the log. Exceptions generated by function execution include caught exceptions (handled errors) and uncaught exceptions (unhandled errors).

#### Solutions


You can log in to the [SCF console](https://console.cloud.tencent.com/scf/index) and follow the steps below to test exception handling:

1. Create a function and copy the following function code without adding any triggers.
2. Click **Test** in the console and select the "Hello World" test sample for testing.

This document provides the following three ways to throw exceptions, and you can choose how to handle exceptions in the code based on your actual needs.
<dx-tabs>
::: Throw exceptions explicitly

**Sample**

```python
def always_failed_handler (event,context):
    raise Exception ('I failed!')
```

**Description**
This function will throw an exception during execution and return the following error message. The SCF platform will record this error message in the function log.

```
File "/var/user/index.py", line 2, in always_failed_handler
raise Exception ('I failed!')
Exception: I failed!
```

:::
::: Inherit the `Exception` class

**Sample**

```python
class UserNameAlreadyExistsException (Exception): pass
def create_user (event):
    raise UserNameAlreadyExistsException ('
		The username already exists,
		please change a name!')
```

**Description**

You can define how to handle errors in your code to ensure the robustness and scalability of your application.

:::
::: Use the `Try` statement to capture errors

**Sample**

```python
def create_user (event):
    try:
        createUser (event [username],event [pwd])
    except UserNameAlreadyExistsException,e: //catch error and do something
```

**Description**

You can define how to handle errors in your code to ensure the robustness and scalability of your application.

:::
</dx-tabs>

#### Returned error message

If exception handling and error capture are not performed in your code logic, the SCF platform will capture errors as much as possible such as when your function suddenly crashes and exits during execution. The platform will return a general error message if it cannot capture an error that occurs.
The table below lists some common errors in code execution:

| Error Scenario | Error Message |
| ------------------- | ------------------------------------------------------------ |
| `raise` is used to throw an exception | {File "/var/user/index.py", line 2, in always_failed_handler raise Exception ('xxx') Exception: xxx} |
| The handler does not exist      | {'module' object has no attribute 'xxx'}                     |
| The dependent module does not exist    | {global name 'xxx' is not defined}                           |
| Timed out                | {"time out"}                                                 |

## Logs

The SCF platform stores all the records of function invocations and the outputs of the function code in logs. You can use the printout or log statement in the programming language to generate the output logs for debugging and troubleshooting. For more information, see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).


## Notes

Because of the nature of SCF, you must write your function code in a **stateless** style. State characteristics in the lifecycle of a function such as local file storage will be destroyed after the function invocation ends.
Therefore, we recommend you store persistent states in TDSQL, COS, TencentDB for Memcached, or other cloud storage services.

## Development Process

For more information on the function development process, see [User Guide](https://intl.cloud.tencent.com/document/product/583/45901).




<style>
	.params{
		margin-bottom:0px !important;
	}
</style>
