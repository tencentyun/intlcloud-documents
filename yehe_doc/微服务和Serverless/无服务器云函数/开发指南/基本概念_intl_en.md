Serverless Cloud Function (SCF) provides two deployment methods of code deployment and image deployment and supports two function types of event-triggered function and HTTP-triggered function. Different deployment methods and function types require different specifications during code development. This document describes the writing specifications and related concepts of event-triggered function in code deployment. For more information on [image deployment](https://intl.cloud.tencent.com/document/product/583/41076) and [HTTP-triggered function](https://intl.cloud.tencent.com/document/product/583/40688), please see the corresponding documents.

An SCF event-triggered function involves three basic concepts: execution method, function input parameter, and function return.

<dx-alert infotype="notice" title="">
The above concepts correspond respectively to the following in general project development:
**Execution method**: corresponds to the main function of the project and is the starting point of program execution.
**Function input parameter**: refers to function input parameters in a normal sense. However, in the SCF environment, the input parameters of an entry function are fixed values. For more information, please see [Function Input Parameters](#input).
**Function return**: corresponds to the returned value of the main function in the project. After the function returns, the code execution ends.
</dx-alert>



## Execution Method
When the SCF platform invokes a function, it will first find an execution method as the entry point to execute your code. At this time, you need to set in the format of **filename.execution method name**.
For example, if the user-configured execution method is `index.handler`, the SCF platform will first look for the `index` file in the code package and find the `handler` method in the file to start execution.
In the execution method, you can process the input parameters of the entry function and call other methods in the code arbitrarily. In SCF, the completion of the execution of the entry function or the exception of the execution of the function marks the end of execution.


## Function Input Parameters[](id:input)

Function input parameters refer to the content that is passed to the function when the function is triggered. Usually, there are two input parameters: `event` and `context`. However, the number of input parameters may vary by programming language and environment. For more information, please see [Serverless Cloud Function](https://intl.cloud.tencent.com/document/product/583/40190).
<dx-tabs>
::: event

#### Usage
The `event` parameter is of `dict` type and contains the basic information that triggers the function. It can be in a platform-defined or custom format. After the function is triggered, the event can be processed inside the code.
#### Instructions
There are two ways to trigger an SCF function:
1. Trigger by calling [TencentCloud API](https://intl.cloud.tencent.com/document/product/583/17243).
2. Trigger by binding a [trigger](https://intl.cloud.tencent.com/document/product/583/9705). 

These two SCF trigger methods correspond to two event formats:
- TencentCloud API:
You can freely define a parameter of `dict` type between the invoker and the function code, where the invoker passes in the data in the format agreed upon, and the function code gets the data in the format.
**Sample:**
You can define a data structure `{"key":"XXX"}` of `dict` type, and when the invoker passes in the data `{"key":"abctest"}`, the function code can get the value `abctest` through `event[key]`.

- Trigger:
  SCF can be connected with various Tencent Cloud services such as API Gateway, COS, and CKafka, so you can bind a corresponding Tencent Cloud service trigger to a function. When the function is triggered, the service will pass the event to SCF as the `event` parameter in a platform-predefined unchangeable format. You can write code based on this format and get information from the `event` parameter.
  **Sample:**
  When COS triggers a function, the specific information of the bucket and the file will be passed to the `event` parameter in <a href="https://intl.cloud.tencent.com/document/product/583/9707">JSON</a> format. The processing of the triggering event can be completed by parsing the `event` information in the function code.
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
</table>



<dx-alert infotype="notice" title="">
To ensure compatibility, the descriptions of the namespace at different stages of the SCF function are retained in the context.
 The content of the context structure may be increased as the SCF platform is iterated.
</dx-alert>


You can print the context information through the standard output statement in the function code. Take the `python` runtime environment as an example:

``` Python
# -*- coding: utf8 -*-
import json
def main_handler(event, context):
    print(context)
    return("Hello World")
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
	<li>To ensure uniformity for each programming language and environment, `event` and `context` should be uniformly encapsulated in the `JSON` data format.</li>
	<li>Different triggers pass different data structures when triggering functions. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/583/9705">Trigger Overview</a>.</li>
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
<li>If triggered by API Gateway or the TencentCloud API for sync invocation, the function will be triggered synchronously.</li>
		<li>For a function triggered synchronously, the SCF platform will not return the trigger result during function execution.</li>
		<li>After the function is executed, the SCF platform will encapsulate the returned value into JSON format and return it to the invoker.</li>
		</ul>
	</td>
	</tr>
	<tr>
	<td>Async triggering</td>
	<td>
		<ul class="params">
	<li>For a function that is triggered asynchronously, the SCF will return the triggering request ID after receiving the triggering event.</li>
			<li>After the function is executed, the returned value will be encapsulated into JSON format and stored in the log.</li>
			<li>After the function execution is completed, you can query the log by the request ID in the return to get the returned value of the asynchronously triggered function.</li>
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


You can log in to the [SCF console](https://console.cloud.tencent.com/scf/index) and follow the steps below to test exception handling:
1. Create a function and copy the following function code without adding any triggers.
2. Click **Test** in the console and select the "Hello World" test sample for testing.

This document provides the following three ways to throw exceptions, and you can choose how to handle exceptions in the code based on your actual needs.
<dx-tabs>
::: Throw exceptions explicitly

**Sample**

```python
def always_failed_handler(event,context):
    raise Exception('I failed!')
```
**Description**
This function will throw an exception during execution and return the following error message. The SCF platform will record this error message in the function log.

```
File "/var/user/index.py", line 2, in always_failed_handler
raise Exception('I failed!')
Exception: I failed!
```
:::
::: Inherit the `Exception` class

**Sample**

```python
class UserNameAlreadyExistsException(Exception): pass
def create_user(event):
    raise UserNameAlreadyExistsException('
		The username already exists,
		please change a name!')
```

**Description**

You can define how to handle errors in your code to ensure the robustness and scalability of your application.

:::
::: Use the `Try` statement to capture errors

**Sample**

```python
def create_user(event):
    try:
        createUser(event[username],event[pwd])
    except UserNameAlreadyExistsException,e: //catch error and do something
```

**Description**

You can define how to handle errors in your code to ensure the robustness and scalability of your application.

:::
</dx-tabs>

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
The SCF platform stores all the records of function invocations and the outputs of the function code in logs. You can use the printout or log statement in the programming language to generate the output logs for debugging and troubleshooting. For more information, please see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).


## Notes
Because of the nature of SCF, you must write your function code in a **stateless** style. State characteristics in the lifecycle of a function such as local file storage will be destroyed after the function invocation ends.
Therefore, you are recommended to store persistent states in TDSQL, COS, TencentDB for Memcached, or other cloud storage services.

## Development Process
For more information on the function development process, please see [Getting Started](https://intl.cloud.tencent.com/document/product/583/9179).




<style>
	.params{
		margin-bottom:0px !important;
	}
</style>
