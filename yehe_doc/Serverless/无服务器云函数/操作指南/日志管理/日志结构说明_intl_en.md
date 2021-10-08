SCF logs are written into CLS by log. Each request is logged in multiple logs, and each log is in a fixed `key:value` format.

## Key-Value Format of Single Log

### Default format

In the default format, each log consists of 14 fixed `key:value` pairs as shown below:

<table>
<thead>
<tr>
<th>Field</th>
<th>Field Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>SCF_FunctionName</td>
<td>text</td>
<td>Function name.</td>
</tr>
<tr>
<td>SCF_Namespace</td>
<td>text</td>
<td>Function namespace.</td>
</tr>
<tr>
<td>SCF_StartTime</td>
<td>long</td>
<td>Invocation start time.</td>
</tr>
<tr>
<td>SCF_LogTime</td>
<td>long</td>
<td>Log generation time.</td>
</tr>
<tr>
<td>SCF_RequestId</td>
<td>text</td>
<td>Request ID.</td>
</tr>
<tr>
<td>SCF_Duration</td>
<td>long</td>
<td>Function execution duration.</td>
</tr>
<tr>
<td>SCF_Alias</td>
<td>text</td>
<td>Alias.</td>
</tr>
<tr>
<td>SCF_Qualifier</td>
<td>text</td>
<td>Version.</td>
</tr>
<tr>
<td>SCF_MemUsage</td>
<td>double</td>
<td>Function execution memory.</td>
</tr>
<tr>
<td>SCF_Level</td>
<td>text</td>
<td>Log4J log level. Default value: INFO.</td>
</tr>
<tr>
<td>SCF_Message</td>
<td>text</td>
<td>Log content.</td>
</tr>
<tr>
<td>SCF_Type</td>
<td>text</td>
<td>Log type. Platform: platform log; Custom: user log.</td>
</tr>
<tr>
<td>SCF_StatusCode</td>
<td>long</td>
<td>Function execution <a href="https://intl.cloud.tencent.com/document/product/583/35311">status code</a>.</td>
</tr>
<tr>
<td>SCF_RetryNum</td>
<td>long</td>
<td>Number of retries.</td>
</tr>
</tbody></table>




### Simplified format

In the simplified format, there are fewer key-value pairs than in the default format, where only the fields required in log query scenarios are retained. In this format, logs are divided into user logs and platform logs with different specific formats as shown below:

#### User log

A user log is a user's standard output in the code, which the platform will capture and report to CLS.

<table>
<thead>
<tr>
<th>Field</th>
<th>Field Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>SCF_FunctionName</td>
<td>text</td>
<td>Function name.</td>
</tr>
<tr>
<td>SCF_Namespace</td>
<td>text</td>
<td>Function namespace.</td>
</tr>
<tr>
<td>SCF_LogTime</td>
<td>long</td>
<td>Log generation time.</td>
</tr>
<tr>
<td>SCF_RequestId</td>
<td>text</td>
<td>Request ID.</td>
</tr>
<tr>
<td>SCF_Alias</td>
<td>text</td>
<td>Alias.</td>
</tr>
<tr>
<td>SCF_Qualifier</td>
<td>text</td>
<td>Version.</td>
</tr>
<tr>
<td>SCF_Message</td>
<td>text</td>
<td>Log content.</td>
</tr>
<tr>
<td>SCF_Type</td>
<td>text</td>
<td>Log type. Platform: platform log; Custom: user log.</td>
</tr>
<tr>
<td>SCF_RetryNum</td>
<td>long</td>
<td>Number of retries.</td>
</tr>
</tbody></table>




#### Platform log

A platform log is the log printed at the start or end of each request. It is used to mark the start and end of a request and record its execution. Platform logs cannot be canceled.

There are two key-value compositions of platform logs. The key-value composition of `report` logs that record request execution is as shown in Table 1 below, and that of other platform logs (such as `START`, `END`, `ERROR`, and `Response`) are in Table 2 below.
<dx-tabs>
::: Table 1

| Field         | Field Type | Description                                                     |
| ---------------- | -------- | ------------------------------------------------------------ |
| SCF_FunctionName | text     | Function name.                                                   |
| SCF_Namespace    | text     | Function namespace.                                           |
| SCF_StartTime    | long     | Invocation start time.                                               |
| SCF_LogTime      | long     | Log generation time.                                               |
| SCF_RequestId    | text     | Request ID.                                                    |
| SCF_Duration     | long     | Function execution duration.                                               |
| SCF_Alias        | text     | Alias.                                                       |
| SCF_Qualifier    | text     | Version.                                                       |
| SCF_MemUsage     | double   | Function execution memory.                                               |
| SCF_Level        | text     | Log4J log level. Default value: INFO.                                |
| SCF_Message      | text     | Log content.                                                   |
| SCF_Type         | text     | Log type. Platform: platform log; Custom: user log.            |
| SCF_StatusCode   | long     | Function execution [status code](https://intl.cloud.tencent.com/document/product/583/35311). |
| SCF_RetryNum     | long     | Number of retries.                                                   |

:::
::: Table 2
<table>
<thead>
<tr>
<th>Field</th>
<th>Field Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>SCF_FunctionName</td>
<td>text</td>
<td>Function name.</td>
</tr>
<tr>
<td>SCF_Namespace</td>
<td>text</td>
<td>Function namespace.</td>
</tr>
<tr>
<td>SCF_StartTime</td>
<td>long</td>
<td>Invocation start time.</td>
</tr>
<tr>
<td>SCF_LogTime</td>
<td>long</td>
<td>Log generation time.</td>
</tr>
<tr>
<td>SCF_RequestId</td>
<td>text</td>
<td>Request ID.</td>
</tr>
<tr>
<td>SCF_Alias</td>
<td>text</td>
<td>Alias.</td>
</tr>
<tr>
<td>SCF_Qualifier</td>
<td>text</td>
<td>Version.</td>
</tr>
<tr>
<td>SCF_Message</td>
<td>text</td>
<td>Log content.</td>
</tr>
<tr>
<td>SCF_Type</td>
<td>text</td>
<td>Log type. Platform: platform log; Custom: user log.</td>
</tr>
<tr>
<td>SCF_RetryNum</td>
<td>long</td>
<td>Number of retries.</td>
</tr>
</tbody></table>
:::
</dx-tabs>





### Log format selection and switch

You can edit the function configuration and select or switch the log format in **Log Configuration** > **Log Format**.

![](https://main.qcloudimg.com/raw/b15cc9a31507cf1464789f6726108eff.png)

> !
>
> - The log configuration is at the function level, and the updated configuration will take effect immediately for both the `$LATEST` version and published versions.
> - Currently, the [GetFunctionLogs](https://intl.cloud.tencent.com/document/product/583/18583) API doesn't support querying logs in simplified format.
> - Compared with the default format, the simplified format can reduce the fees incurred by logs, but information such as execution duration and memory during function execution will no longer be displayed in real time.
> - The simplified format is only supported for non-image-based event functions.



## Log Structure of Single Request

There are two log structures for one single SCF request: invocation log and provisioning log.

<dx-tabs>
::: Invocation log structure
SCF invocation logs use platform logs to mark the request start and end, request error message, function return, and request execution, and user logs are encapsulated between the start and end of the request. The log structure is as follows (the table only shows the `SCF_Message` field as an example):

<table>
<thead>
<tr>
<th>SCF_Message</th>
<th>Log Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>START RequestId:09c346d3-8417-49c5-8569-xxxxxxxxxxxx</td>
<td>Platform log</td>
<td>Request start.</td>
</tr>
<tr>
<td>init log</td>
<td>User log</td>
<td>The log content printed by the user during function initialization. The container will execute the initialization logic only in case of cold start, and no initialization logs will be output in non-cold start scenarios.</td>
</tr>
<tr>
<td>Init Report RequestId: 09c346d3-8417-49c5-8569-xxxxxxxxxxxx InitDuration: 4598ms Duration: 3924ms Memory: 640MB MemUsage: 57.86MB</td>
<td>Platform log</td>
<td>Initialization execution log. `InitDuration` is the initialization duration, `Duration` is the duration of user business logic during initialization and smaller than `InitDuration`, `Memory` is the configured function memory size, and `MemUsage` is the execution memory size during initialization.<br>The container will execute the initialization logic only in case of cold start, and no initialization logs will be output in non-cold start scenarios.</td>
</tr>
<tr>
<td>invoke log</td>
<td>User log</td>
<td>The log content printed by the user during function invocation.</td>
</tr>
<tr>
<td>ERROR RequestId:09c346d3-8417-49c5-8569-xxxxxxxxxxxx Result:xxx</td>
<td>Platform log</td>
<td>Function error cause. There will be no ERROR logs when the function is executed properly.</td>
</tr>
<tr>
<td>Response RequestId:09c346d3-8417-49c5-8569-xxxxxxxxxxxx RetMsg:"Hello World"</td>
<td>Platform log</td>
<td>The function return is recorded in `RetMsg`.</td>
</tr>
<tr>
<td>END RequestId:09c346d3-8417-49c5-8569-xxxxxxxxxxxx</td>
<td>Platform log</td>
<td>Request end.</td>
</tr>
<tr>
<td>Report RequestId:09c346d3-8417-49c5-8569-c55033b17f51 Duration:1ms Memory:128MB MemUsage:29.734375MB</td>
<td>Platform log</td>
<td>Function invocation execution log. `Duration` is the function execution duration, `Memory` is the configured function memory size, and `MemUsage` is the execution memory size during function execution.</td>
</tr>
</tbody></table>



<dx-alert infotype="notice" title="">
Initialization logs and instance provisioning logs are only supported for web functions and image-based functions and are currently in beta test by region.
</dx-alert>
Below is the sample code for printing one line of initialization log and one line of invocation log of a web function in the `Python` runtime environment:
<dx-codeblock>
:::  python

```python
from flask import Flask
app = Flask(__name__)
print("init log")

@app.route('/')
def hello_world():
   return 'Hello World'

if __name__ == '__main__':
   app.run(host='0.0.0.0',port=9000)
```

:::
</dx-codeblock>
The output log structure is as follows (only the content of the `SCF_Message` field is displayed):
<dx-codeblock>
:::  log

``` 
START RequestId:09c346d3-8417-49c5-8569-xxxxxxxxxxxx
 * Serving Flask app "app" (lazy loading)
 * Environment: production
 WARNING: Do not use the development server in a production environment.
 Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://0.0.0.0:9000/ (Press CTRL+C to quit)
init log
Init Report RequestId:09c346d3-8417-49c5-8569-xxxxxxxxxxxx InitDuration: 2235ms Duration: 1235ms Memory: 640MB MemUsage: 5.21MB
Hello world
Response RequestId:09c346d3-8417-49c5-8569-xxxxxxxxxxxx RetMsg:"Hello World"
END RequestId:09c346d3-8417-49c5-8569-xxxxxxxxxxxx
Report RequestId:09c346d3-8417-49c5-8569-xxxxxxxxxxxx Duration:1ms Memory:128MB MemUsage:29.734375MB
```


:::
</dx-codeblock>
:::
::: Provisioning log structure
SCF provisioning logs start by user log printing and end by provisioning marking in platform log. The log structure is as follows (the table only shows the `SCF_Message` field as an example):

<table>
<thead>
<tr>
<th>SCF_Message</th>
<th>Log Type</th>
<th>Description</th>
<tr>
<td>provision log</td>
<td>User log</td>
<td>The log content printed by the user during function initialization, which will be recorded in a log in instance provisioning scenarios.</td>
</tr>
<tr>
<td>ERROR RequestId:09c346d3-8417-49c5-8569-xxxxxxxxxxxx Result:xxx</td>
<td>Platform log</td>
<td>Cause of an instance provisioning failure. There will be no ERROR logs if instance provisioning succeeds.</td>
</tr>
<tr>
<td>Provisioned Report RequestId: c6af0fb4-1c07-4a92-8307-xxxxxxxxxxxx InitDuration: 2286ms Duration: 1208ms Memory: 640MB MemUsage: 5.14MB</td>
<td>Platform log</td>
<td>Instance provisioning execution log. `InitDuration` is the initialization duration, i.e., instance provisioning duration. `Duration` is the duration of user business logic during initialization, i.e., duration of user business logic during instance provisioning.<br>`Duration` is smaller than `InitDuration`. `Memory` is the configured function memory size. `MemUsage` is the execution memory size during provisioning. The log will be output only in provisioning scenarios.</td>
</tr>
</tbody></table>



<dx-alert infotype="notice" title="">
 Instance provisioning logs are only supported for web functions and image-based functions and are currently in beta test by region.
</dx-alert>


Below is the sample code for printing one line of initialization log and one line of invocation log of a web function in the `Python` runtime environment:
<dx-codeblock>

:::  python

```python
from flask import Flask
app = Flask(__name__)
print("init log")

@app.route('/')
def hello_world():
   return 'Hello World'

if __name__ == '__main__':
   app.run(host='0.0.0.0',port=9000)
```

:::
</dx-codeblock>
The output log structure in instance provisioning scenarios is as follows (only the content of the `SCF_Message` field is displayed):
<dx-codeblock>
:::  log

``` 
 * Serving Flask app "app" (lazy loading)
 * Environment: production
 WARNING: Do not use the development server in a production environment.
 Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://0.0.0.0:9000/ (Press CTRL+C to quit)
init log
Previsioned Report RequestId:09c346d3-8417-49c5-8569-xxxxxxxxxxxx InitDuration: 2235ms Duration: 1235ms Memory: 640MB MemUsage: 5.21MB
```

:::
</dx-codeblock>
:::

</dx-tabs>
