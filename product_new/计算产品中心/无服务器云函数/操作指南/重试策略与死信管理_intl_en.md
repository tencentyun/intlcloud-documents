
## Retry Policy
A function invocation may fail due to various reasons. The SCF platform has the following built-in retry policies that can automatically retry invocation failure events.

### Platform errors
**Error types**: Internal platform error, insufficient computing resource, etc.

**Retry policy**: Continuous retry. When the SCF backend receives an alarm, it will retry the current invocation failure event by exponential backoff. When the retry interval exceeds 1 hour, it will retry once every other hour for 24 hours. If you have configured a dead letter queue, events that still fail after such time lapses will be sent to the dead letter queue for further processing on your own; otherwise, they will be deleted by the SCF platform.

### User errors
**Error types**: Code error, execution timeout, resource overrun, etc.

**Retry policy**: After an invocation fails, the function will automatically retry twice where the first retry will occur 1 minute after the failure and the second retry 2 minutes after the first retry. While automatically retrying, the function can still handle new trigger events normally. If a dead letter queue is configured, events of three consecutive failures will be passed to the queue; otherwise, the events will be deleted by the SCF platform.

## Dead Letter Queue
According to the retry rules of SCF, events that still fail after the configured number of retries will be discarded or delivered to the user-defined dead letter queue (a CMQ topic or queue). The dead letter queue is configured on your own to collect error time information and analyze causes of failures. If no dead letter queue is configured for a function, the function will discard such events.

### Message attributes in the dead letter queue
- **RequestID**: Unique event ID
- **ErrorCode**: Event error code
- **ErrorMessage**: Error message

## Dead Letter Queue Creation Process
>SCF currently supports a CMQ topic or queue as the dead letter queue for your choice.
>
1. Log in to the [CMQ Console](https://console.cloud.tencent.com/cmq/index?rid=1) and create a dead letter queue.
>If the topic mode is selected, a message in the dead letter queue may not reach its destination through a topic due to filter settings. CMQ supports two filtering schemes: tag filtering and route matching.
>To ensure that your subscribers can receive all error messages, when adding a subscriber, please leave the tag filter **blank**; for BindingKey filtering,
>enter **"#"**.
>
2. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) and create a function.
 The executor role of the function must have access permission to the CMQ topic and queue, which has already been configured for the default executor role in SCF. If you use a custom role, be sure to grant it such permission. You can configure the dead letter queue on the **Create Function** or **Configure Function** page.




