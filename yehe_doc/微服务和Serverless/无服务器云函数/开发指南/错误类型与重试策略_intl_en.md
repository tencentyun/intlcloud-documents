A function invocation may fail for various reasons. Different **error types** and **invocation methods (sync or async invocation)** all affect the retry policy. You can configure a [dead letter queue (DLQ)](#DLQ) to collect error event information and analyze causes of failures.

## Error Types
A function invocation may fail for various reasons. The errors can be divided into the following types:

### Invocation error
An invocation error occurs before the function is actually executed. It will occur in the following cases:
- **Invocation request error**. For example, the data structure of the event passed in is too large, an input parameter does not meet the requirements, or the function does not exist.
- **Invoker error**. This error generally occurs when the invoker does not have required permissions.
- **Overrun error**. The number of concurrent invocations exceeds the [maximum concurrency](https://intl.cloud.tencent.com/document/product/583/39848) limit.

### Execution error
An execution error occurs during the actual execution of a function. It will occur in the following cases:
  * **User code execution error**. This type of errors occurs during the execution of user code; for example, the function code throws an exception, or the format of the returned result is exceptional.
  * **Runtime error**. During function execution, the runtime is responsible for pulling and executing user code. A runtime error refers to errors detected and reported by the runtime, such as function execution timeout (for the timeout period, see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637)) and code syntax error.

### System error
It refers to errors of the function platform, such as internal error.

## Retry Policy
Different **error types** and **invocation methods (sync or async invocation)** all affect the retry policy.

### Sync invocation
Types of sync invocation include sync invocation by [TencentCloud API trigger](https://intl.cloud.tencent.com/document/product/583/18198), [API Gateway trigger](https://intl.cloud.tencent.com/document/product/583/12513), [CKafka trigger](https://intl.cloud.tencent.com/document/product/583/17530), and [CLB trigger](https://intl.cloud.tencent.com/document/product/583/39849).
In sync invocation, the error message will be directly returned; therefore, when an error occurs in sync invocation, the platform will not automatically retry, and the retry policy (i.e., whether to retry and the number of retries) will be determined by the invoker.

>! A CKafka trigger will create a backend module as a consumer that can connect to a CKafka instance and consume messages. After obtaining the message, the backend module will synchronously invoke the triggered function. Since the backend module of the CKafka trigger is maintained by SCF, the retry policy for sync invocation will also be controlled by SCF.
>- For execution errors (including user code errors and runtime errors), the CKafka trigger will retry according to the configured retry times, which is 10,000 by default.
>- For overrun errors and system errors, the CKafka trigger will continue to retry in an exponential backoff manner until it succeeds.

### Async invocation
Types of async invocation include async invocation by [TencentCloud API trigger](https://intl.cloud.tencent.com/document/product/583/18198), [COS trigger](https://intl.cloud.tencent.com/document/product/583/9707), [scheduled trigger](https://intl.cloud.tencent.com/document/product/583/9708), [CMQ topic trigger](https://intl.cloud.tencent.com/document/product/583/11517), etc. For specific trigger invocation types, see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).
You can modify and customize the default **retry attempts** and **maximum waiting time** in the function configuration according to your business needs. This configuration is only applicable to async invocations.
	![](https://main.qcloudimg.com/raw/50b8fd754e102e568eb6ec1dd60012fd.png)
	
  * **Retry Attempts:** the number of times the function retries when an error is returned. This parameter is only applicable to the policy configuration for **execution errors**. The default value is 2 retries.
  * **Maximum Event Age:** the maximum time that the function keeps events in the async event queue. This parameter is applicable to the retry configuration of all async invocations. The default value is 6 hours, and the maximum queue length can reach up to 100,000 events.

Async invocation retry policies for different types of errors:

<table>
<thead>
<tr>
<th>Error Type</th>
<th>Retry Policy</th>
</tr>
</thead>
<tbody>
<tr>
<td>System error</td>
<td>The function request execution status code is 500. When an error of this type occurs, the SCF platform will retry for the configured maximum event age (which is 6 hours by default) at intervals of one minute. If a DLQ is configured, events that still fail after the maximum event age elapses will be sent to it for further processing on your own; otherwise, they will be discarded by the SCF platform.</td>
</tr>
<tr>
<td>Overrun error</td>
<td>The function request execution status code is 432. When an error of this type occurs, the SCF platform will retry for the configured maximum event age (which is 6 hours by default) at intervals of one minute. If a DLQ is configured, events that still fail after the maximum event age elapses will be sent to it for further processing on your own; otherwise, they will be discarded by the SCF platform.</td>
</tr>
<tr>
<td>Execution errors<br>(except system errors and overrun errors, all other errors are execution errors)</td>
<td>When an error of this type occurs, the SCF platform will retry for the configured number of retries at intervals of one minute. While automatically retrying, the function can still handle new triggering events normally. If a DLQ is configured, events that still fail after retries for the configured number of times or exceed the maximum waiting time will be passed to it; otherwise, the events will be discarded by the SCF platform.</td>
</tr>
</tbody></table>

>! 
>1. Due to the differences in execution mechanisms, the retry and dead letter queue configurations don't work for errors during the execution of [asynchronously executed functions](https://intl.cloud.tencent.com/document/product/583/39466).
>2. How to judge whether the maximum waiting time is exceeded: if event retry time - event initial trigger time is greater than the maximum waiting time, the maximum waiting time is exceeded.
