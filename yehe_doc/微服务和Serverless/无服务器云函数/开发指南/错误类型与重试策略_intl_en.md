A function invocation may fail for various reasons. Different **error types** and **invocation methods (sync or async invocation)** all affect the retry policy. You can configure a [dead letter queue (DLQ)](#死信队列文档) to collect error event information and analyze causes of failures.

## Error Type
A function invocation may fail for various reasons. The errors can be divided into the following types:

### Invocation error
An invocation error occurs before the function is actually executed. It will occur in the following cases:
  * **Invocation request error**. For example, the data structure of the event passed in is too large, an input parameter does not meet the requirements, or the function does not exist.
  * **Invoker error**. This error generally occurs when the invoker has no sufficient permissions.
  * **Overrun error**. The number of concurrent invocations exceeds the [maximum concurrency](https://intl.cloud.tencent.com/document/product/583/11637) limit.

### Execution error
An execution error occurs during the actual execution of a function. It will occur in the following cases:
  * **User code execution error**. This type of errors occurs during the execution of user code; for example, the function code throws an exception, or the format of the returned result is exceptional.
  * **Runtime error**. During function execution, the runtime is responsible for pulling and executing user code. A runtime error refers to errors detected and reported by the runtime, such as function execution timeout (for the timeout period, please see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637)) and code syntax error.

### System error
It refers to errors of the function platform, such as internal error.

## Retry Policy
Different **error types** and **invocation methods (sync or async invocation)** all affect the retry policy.

### Sync invocation
Types of sync invocation include sync invocation by [TencentCloud API trigger](https://intl.cloud.tencent.com/document/product/583/18198), [API Gateway trigger](https://intl.cloud.tencent.com/document/product/583/12513), and [CKafka trigger](https://intl.cloud.tencent.com/document/product/583/17530).
In sync invocation, the error message will be directly returned; therefore, when an error occurs in sync invocation, the platform will not automatically retry, and the retry policy (i.e., whether to retry and the number of retries) will be determined by the invoker.

>! A CKafka trigger will create a backend module as a consumer that can connect to a CKafka instance and consume messages. After obtaining the message, the backend module will synchronously invoke the triggered function. Since the backend module of the CKafka trigger is maintained by SCF, the retry policy for sync invocation will also be controlled by SCF.
>- For execution errors (including user code errors and runtime errors), the CKafka trigger will retry according to the configured retry times, which is 10,000 by default.
>- For overrun errors and system errors, the CKafka trigger will continue to retry in an exponential backoff manner until it succeeds.

### Async invocation
Types of async invocation include async invocation by [TencentCloud API trigger](https://intl.cloud.tencent.com/document/product/583/18198), [COS trigger](https://intl.cloud.tencent.com/document/product/583/9707), [scheduled trigger](https://intl.cloud.tencent.com/document/product/583/9708), [CMQ topic trigger](https://intl.cloud.tencent.com/document/product/583/11517), etc. For specific trigger invocation types, please see the relevant trigger documentation.
You can modify and customize the default **retry attempts** and **maximum waiting time** in the function configuration according to your business needs. This configuration is only applicable to async invocations.
	![](https://main.qcloudimg.com/raw/50b8fd754e102e568eb6ec1dd60012fd.png)
	
  * **Retry Attempts:** the number of times the function retries when an error is returned. This parameter is only applicable to the policy configuration for **execution errors**. The default value is 2 retries.
  * **Maximum Waiting Time:** the maximum time that the function keeps events in the async event queue. This parameter is applicable to the retry configuration of all async invocations. The default value is 6 hours, and the maximum queue length can reach up to 100,000 events.

Async invocation retry policies for different types of errors:



<table>
<thead>
<tr>
<th>Error Type</th>
<th>Retry Policy</th>
</tr>
</thead>
<tbody><tr>
<td>Execution error<br>(User code execution error and runtime error)</td>
<td>When an error of this type occurs, the SCF platform will retry twice by default or for the configured number of retries at intervals of one minute. While automatically retrying, the function can still handle new triggering events normally. If a DLQ is configured, events with three consecutive failures will be passed to it; otherwise, the events will be discarded by the SCF platform.</td>
</tr>
<tr>
<td>System error</td>
<td>When an error of this type occurs, the SCF platform will retry for the configured maximum waiting time (which is 6 hours by default), and the retry interval will increase to 5 minutes by exponential backoff. If a DLQ is configured, events that still fail after the maximum waiting time elapses will be sent to it for further processing on your own; otherwise, they will be discarded by the SCF platform.</td>
</tr>
<tr>
<td>Overrun error</td>
<td>When an error of this type occurs, the SCF platform will retry for the configured maximum waiting time (which is 6 hours by default) at intervals of one minute. If a DLQ is configured, events that still fail after the maximum waiting time elapses will be sent to it for further processing on your own; otherwise, they will be discarded by the SCF platform.</td>
</tr>
<tr>
<td>Invocation request and invoker errors</td>
<td>When an error of this type occurs, the system will not retry except for <strong>overrun errors</strong>, as retries will not succeed by nature.</td>
</tr>
</tbody></table>
