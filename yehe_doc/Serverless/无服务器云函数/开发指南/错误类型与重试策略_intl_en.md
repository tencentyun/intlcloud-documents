A function invocation may fail for various reasons. Different **error types** and **invocation methods (sync or async invocation)** all affect the retry policy. You can configure a dead letter queue to collect error event information and analyze causes of failures.

## Error Type
A function invocation may fail for various reasons. The errors can be divided into the following types:

### **Invocation error**
An invocation error occurs before the function is actually executed. It will occur in the following cases:
  * **Invocation request error**. For example, the data structure of the event passed in is too large, an input parameter does not meet the requirements, or the function does not exist.
  * **Invoker error**. This error generally occurs when the invoker has no sufficient permissions.
  * **Overrun error**. The number of invocation concurrences exceeds the [maximum concurrence](https://intl.cloud.tencent.com/document/product/583/11637).

### **Execution error**
An execution error occurs during the actual execution of a function. It will occur in the following cases:
  * **User code execution error**. This type of errors occurs during the execution of user code; for example, the function code throws an exception, or the format of the returned result is exceptional.
  * **Runtime error**. During function execution, the runtime is responsible for pulling and executing user code. A runtime error refers to errors detected and reported by the runtime, such as function execution timeout (for the timeout period, please see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637)) and code syntax error.
  
### **System error**
It refers to errors of the function platform, such as internal error.

## Retry Policy
Different **error types** and **invocation methods (sync or async invocation)** all affect the retry policy.

### Sync invocation
There are three types of sync invocation: sync invocation by [TencentCloud API trigger](https://intl.cloud.tencent.com/document/product/583/18198), [API Gateway trigger](https://intl.cloud.tencent.com/document/product/583/12513), and [CKafka trigger](https://intl.cloud.tencent.com/document/product/583/17530).
In sync invocation, the error message will be directly returned; therefore, when an error occurs in sync invocation, the platform will not automatically retry, and the retry policy (i.e., whether to retry and the number of retries) will be determined by the invoker.

### Async invocation
There are four types of async invocation: async invocation by [TencentCloud API trigger](https://intl.cloud.tencent.com/document/product/583/18198), [COS trigger](https://intl.cloud.tencent.com/document/product/583/9707), [timer trigger](https://intl.cloud.tencent.com/document/product/583/9708), and [CMQ topic trigger](https://intl.cloud.tencent.com/document/product/583/11517).
When the following types of errors occur in async invocation, the retry policies will be as follows:
  - **Execution error** (**user code execution error** or **runtime error**): when an error of this type occurs, the SCF platform will automatically retry twice, where the first retry will occur 1 minute after the original event and the second one 2 minutes after the first one. While automatically retrying, the function can still handle new trigger events normally. If a dead letter queue is configured, events with three consecutive failures will be passed to the queue; otherwise, the events will be discarded by the SCF platform.
  - **Overrun error** and **system error**: when an error of this type occurs, the SCF platform will retry for 24 hours, and the retry interval will increase to 1 hour by exponential backoff. If a dead letter queue is configured, events that still fail after 24 hours of retries will be sent to the dead letter queue for further processing on your own; otherwise, they will be discarded by the SCF platform.
  - **Invocation request error** and **invoker error**: when an error of this type occurs, the SCF platform will not retry, because events that fail due to this type of errors will not succeed even after retries.

## Dead Letter Queue
A dead letter queue is a CMQ queue under your account that is used to collect error event information and analyze causes of failures. If you have configured a dead letter queue for a function, when an event still fails after the SCF platform retries it twice due to a **user code execution error** or for more than 24 hours due to an **overrun error** or **system error**, the event will be sent to the dead letter queue.

>The dead letter queue feature is currently in beta test. If you want to try it out, please apply for activation of CMQ.

### Dead letter queue message attributes
- **RequestID**: unique event ID
- **ErrorCode**: event error code
- **ErrorMessage**: error message

### Dead letter queue creation process
>SCF currently supports a CMQ topic or queue as the dead letter queue for your choice.
>
1. Log in to the [CMQ Console](https://console.cloud.tencent.com/cmq/index?rid=1) and create a dead letter queue.
CMQ topics support filtering by tag or route match. To ensure that your subscribers can receive all error messages, when adding a subscriber, please leave the tag filter **empty** and enter **"#"** for the `BindingKey` filter.
2. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) and create a function.
 The executor role of the function must have access permission to the CMQ topic and queue, which has already been configured for the default executor role in SCF. If you use a custom role, be sure to grant it such permission.
3. Configure the dead letter queue.
 You can configure the dead letter queue on the "Create Function" or "Configure Function" page.
