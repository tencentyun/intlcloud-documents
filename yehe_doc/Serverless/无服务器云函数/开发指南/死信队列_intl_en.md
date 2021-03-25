## Overview
A dead letter queue (DLQ) is a message queue under your account used to collect error event information and analyze causes of failures. If you have configured a DLQ for a function, an event will be sent to the DLQ if:
- It still fails after the SCF platform retries it twice due to a **user code execution error**
- It still fails after the SCF platform retries it for more than 24 hours due to an **overrun error** or **system error**
- Message retention in the [async queue](https://intl.cloud.tencent.com/document/product/583/9694) reaches the upper limit.



>?The DLQ feature is currently in beta test. If you want to try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for the activation of CMQ.



## DLQ Message Attributes
- **RequestId**: (string) unique identifier of the event call request
- **ErrorCode**: (numeric) error code status
- **ErrorMessage**: (string) error message

When the DLQ delivers a message to CMQ, it encapsulates the attribute information and event information in a JSON request body in the following format:
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


| Structure | Content |
|---------|---------|
| AppId | APPID.	 |
| Uin | Root account ID.	|
| SubAccountUin | Sub-account ID of the creator (this field may return null, indicating that no valid values can be obtained). 	|
| RequestSource | Trigger request source. |
| FunctionName | Function name. |
| Namespace | Namespace. |
| Qualifier | Version/Alias of the trigger function. |
| ClientContext | Parameters used to run the function, which are passed in JSON format. For the maximum parameter length, please see [Limits](https://intl.cloud.tencent.com/document/product/583/11637). |
| TimeStampForInvoker | The millisecond timestamp when the function is invoked. |
| RequestId | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. |
| PushTime | Time when the message is pushed to CMQ. |
| RetryNum | Number of retries (0–2). |
| Ttl | Retention time of the async queue event. |

## Directions
### Creating DLQ
>?SCF currently supports a CMQ topic or queue as the DLQ for your choice.
>The DLQ of a function alias will follow the DLQ of the primary version, i.e., the first DLQ selected and configured when the alias is created in the console.
>
1. Log in to the [CMQ console](https://console.cloud.tencent.com/cmq/index?rid=1) and create a DLQ.
CMQ topics support filtering by tag or route match. To ensure that your subscribers can receive all error messages, when adding a subscriber, please leave the tag filter **empty** and enter **"#"** for the `BindingKey` filter.
2. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) and create a function.
3. Configure the DLQ.
 You can configure the DLQ on the **Create Function** or **Configure Function** page.


### Monitoring DLQ

When using a DLQ, permission errors, incorrect resource configurations, or message sizes exceeding the size limit of the target queue or topic will cause DLQ delivery failures. You can query the "number of failed deliveries to DLQ" in the function monitoring information.
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. Select the region of the function for which to monitor the DLQ at the top of the page and click the target function in the list to enter the function details page.
3. On the function details page, click **Monitoring information** to view the number of failed deliveries to the DLQ.

