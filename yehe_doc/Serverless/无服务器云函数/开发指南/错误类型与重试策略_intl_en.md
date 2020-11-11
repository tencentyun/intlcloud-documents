A function invocation may fail for various reasons. Different **error types** and **invocation methods (sync or async invocation)** affect the retry policy. You can configure a dead letter queue to collect error event information and analyze the causes of failures.

## Error Types
A function invocation may fail for various reasons. Errors can be classified into the following types:

### Invocation error
An invocation error occurs before the function is actually executed. It will occur in the following cases:
  * **Invocation request error**. For example, the data structure of the event passed in is too large, an input parameter does not meet the requirements, or the function does not exist.
  * **Invoker error**. This error generally occurs when the invoker does not have the required permissions.
  * **Overrun error**. The number of invocation concurrences exceeds the [maximum concurrence](https://intl.cloud.tencent.com/document/product/583/11637).

### Execution error
An execution error occurs during the actual execution of a function. It will occur in the following cases:
  * **User code execution error**. This type of errors occurs during the execution of user code. For example, the function code throws an exception, or the format of the returned result is exceptional.
  * **Runtime error**. During function execution, runtime pulls and executes the user code. A runtime error refers to errors detected and reported by runtime, such as function execution timeout (for more information about the timeout limit, please see [Limits](https://intl.cloud.tencent.com/document/product/583/11637)) and code syntax error.

### System error
It refers to errors of the function platform, such as internal error.

## Retry Policy
Different **error types** and **invocation methods (sync or async invocation)** affect the retry policy.

### Sync invocation
There are three types of sync invocation: sync invocation by [TencentCloud API trigger](https://intl.cloud.tencent.com/document/product/583/18198), [API Gateway trigger](https://intl.cloud.tencent.com/document/product/583/12513), and [CKafka trigger](https://intl.cloud.tencent.com/document/product/583/17530).
During sync invocation, the error message is returned to the user directly. Therefore, when an error occurs during sync invocation, the platform will not automatically retry. The retry policy (i.e., whether to retry and the number of retries) will be determined by the invoker.

>! The CKafka trigger creates a backend module as a consumer, connects to the CKafka instance, and consumes messages. When the backend module obtains a message, a function is invoked synchronously. Since SCF maintains the backend module of the CKafka trigger, it controls the retry policy even in sync invocations.
>- For execution errors (including user code execution error and runtime error), the CKafka trigger will perform retry according to your configuration. It retries 10,000 times by default.
>- For overrun and system errors, CKafka continuously retries using an exponential backoff algorithm until the invocation is successful.

### Async invocation
There are four types of async invocation: async invocation by [TencentCloud API trigger](https://intl.cloud.tencent.com/document/product/583/18198), [COS trigger](https://intl.cloud.tencent.com/document/product/583/9707), [timer trigger](https://intl.cloud.tencent.com/document/product/583/9708), and [CMQ topic trigger](https://intl.cloud.tencent.com/document/product/583/11517).
When the following types of errors occur in async invocations, the retry policies will be as follows:
  - **Execution error** (including **user code execution error** and **runtime error**): When an execution error occurs, the SCF platform will automatically retry twice, where the first retry occurs 1 minute after the original event and the second retry occurs 2 minutes after the first retry. During automatically retrying, new triggered events can still be handled normally. If you have configured a dead letter queue, events with three consecutive failures will be passed to the queue; otherwise, the events will be discarded by the SCF platform.
  - **Overrun error** and **system error**: When an error of these types occurs, the SCF platform will retry for 24 hours, and the retry interval will increase to 1 hour according to exponential backoff. If you have configured a dead letter queue, events that still fail after 24 hours of retries will be sent to the dead letter queue so that you can further handle them on your own; otherwise, they will be discarded by the SCF platform.
  - **Invocation request error** and **invoker error**: When an error of these types occurs, the SCF platform will not retry because these types of errors will not succeed even after retrying.

## Dead Letter Queue
Dead letter queue (DLQ) is the CMQ of an account. It collects error event information and the causes of failures. If you have configured dead letter queue for your function, events in the following cases will be sent to the dead letter queue:
* User code execution error occurs and cannot succeed after two retries.
* Overrun error or system error occurs and the retry has been performed for over 24 hours.
* Message retention of [Async queue](https://intl.cloud.tencent.com/document/product/583/9694) has reached the upper limit.

>?The dead letter queue feature is currently in beta test. To try it out, please activate Cloud Message Queue (CMQ).



### Message attributes of dead letter queue
- **RequestID**: (string) a unique identifier of the event invocation request.
- **ErrorCode**: (digit) error code.
- **ErrorMessage**: (string) error message.

When the dead letter queue is passed to CMQ, the attribute information and event information will be encapsulated in a JSON request body formatted as follows:
```
{
  "RequestId": "b615b896-d197-47d7-8919-xxx",
  "ErrorCode": -1,
  "ErrorMessage": "Traceback (most recent call last):\n File \"/var/user/index.py\", line 5, in main_handler\n if 'key1' in event.keys():\nNameError: global name 'event' is not defined",
  "Body": {
    "AppId": xxx,
    "Uin": "xxx",
    "SubAccountUin": "xxx",
    "RequestSource": "TRIGGER_TIMER",
    "FunctionName": "tabortest",
    "Namespace": "default",
    "Qualifier": "$DEFAULT",
    "InvocationType": "RequestResponse",
    "ClientContext": "{\"Type\":\"Timer\",\"TriggerName\":\"tabortimer\",\"Time\":\"2020-10-10T01:22:00Z\",\"Message\":\"\"}",
    "LogType": "",
    "TimeStampForInvoker": "160229310xxx",
    "RequestId": "b615b896-d197-47d7-8919-xxx",
    "PushTime": "2020-10-10T09:22:00.061824591+08:00",
    "RetryNum": 2,
    "Ttl": 0
  }
}
```





### Creating a dead letter queue
>?Currently, SCF supports a CMQ topic or queue as the dead letter queue. You can select one as needed.
>
1. Log in to the [CMQ Console](https://console.cloud.tencent.com/cmq/index?rid=1) and create a dead letter queue.
CMQ topics support filtering by tag or route match. To ensure that your subscribers can receive all error messages, please leave the tag filter **empty** and enter **"#"** for the `BindingKey` filter when adding a subscriber.
2. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) and create a function.
3. Configure the dead letter queue.
 You can configure the dead letter queue on the **Create Function** or **Function configuration** page.

>?The dead letter queue of a function alias will be subjected to that of the master version. Dead letter queue of the master version refers to the first selected and configured dead letter queue when creating the alias on Console.

### Monitoring the dead letter queue

Dead letters may fail to be delivered due to permission error, misallocation of resources, and total message size reaching the limit of target queue or topic. You can go to the **Monitoring information** page on the SCF Console to query the number of dead letter queue delivery errors (`DeadLetterErrors`).
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/index?rid=1) and click **Function Service** in the left sidebar.
2. Choose the region of the function monitored by the expected dead letter queue at the top of the page, and click the function to go to the function detail page. 
3. Click **Monitoring information** on the function detail page to query the number of dead letter queue delivery errors, as shown in the following figure.

