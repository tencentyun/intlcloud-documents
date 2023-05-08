## Use Cases

If a notification message sent by an application contains an error or incorrect redirect link, it will give end users a negative impression of the involved product/service after they view or click it. In this case, you should fix the problem in time. You can choose to terminate, recall, or override the message, or cancel the related scheduled task if there is any. This document describes how to do so through the [console](#console) and [RESTful APIs](#restapi).

## Overview

- Message termination: terminates all offline messages within the offline storage period of the task.
- Message recall: terminates the current message and makes it disappear from the notification center on devices where it has arrived but has not been clicked. A recall is imperceptible to users.
- Message override: terminates the current message and overrides it with a new one. After a successful override, only the new message will be displayed in the device notification center.
- Scheduled task cancellation: Cancels a scheduled task that has not yet been scheduled. After successful cancellation, the scheduled push task will not be delivered any more.

## Use Limits

<table>
<thead>
<tr>
<th>Platform</th>
<th  nowrap="nowrap">Termination</th>
<th>Recall</th>
<th>Override</th>
<th>Scheduled task cancellation</th>
</tr>
</thead>
<tbody><tr>
<td>Android</td>
<td>Supported</td>
<td>This feature is still being upgraded and not available yet.</td>
<td>Supported only for the Tencent Push Notification Service channel, Mi channel, Meizu channel, and Huawei devices on EMUI 10 and later</td>
<td>Supported</td>
</tr>
<tr>
<td>iOS</td>
<td  nowrap="nowrap">Not supported</td>
<td>This feature is still being upgraded and not available yet.</td>
<td>Supported</td>
<td>Supported</td>
</tr>
</tbody></table>

>? Message termination, recall, and override are supported only for notifications whose push target is **push to all devices**, **push to a list of accounts**, or **push to devices with specific tags**.
>Scheduled task cancellation is supported only for notifications whose push target is **push to all devices**, **push by account package**, and **push to devices with specific tags**.
>


<span id="console"></span>

## Using the Console
### Terminating, overriding, or recalling a push task

1. Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns).
2. Click **Message Management** > **Task List** in the left sidebar.
3. Click **View Details** for the push task to be terminated, overridden, or recalled.
4. In the **Push Progress** column in the top-right corner of the push details page, terminate, override, or recall the task.
![](https://main.qcloudimg.com/raw/f6308cf63712ee5a4feecd47f26d7f31.png)
>? When you select message override, for vivo, OPPO, and Huawei (below EMUI 10) devices that do not support message override, you can choose whether to continue the message delivery:
> - If you choose to continue the delivery, the notification message will be overridden, and both the new and original messages will appear in the device notification center at the same time.
> - If you choose to abort the delivery, no new notification messages will be sent to the above devices that do not support message override.
> 
5. After the operation succeeds, you can return to the **Task List** page and view the current status of the task in the **Status** column.

### Cancelling a scheduled task
1. Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns).
2. Click **Message Management** > **Task List** in the left sidebar.
3. Locate the push task whose scheduled task is to be canceled, and click **Cancel Push**.
4. After the operation succeeds, you can see that the status of the push task becomes **Canceled** in the **Status** column.


<span id="restapi"></span>

## Using RESTful APIs

### Message termination

#### API description 

Request method: POST
Request Address
```xml
Service URL/v3/push/stop_push_msg
```

The API service address corresponds to the service access point one by one; therefore, please select the service address corresponding to your application [service access point](https://www.tencentcloud.com/document/product/1024/38517).

#### Request parameters

| Parameter | Type | Required | Description |
| ------ | ------ | -------- | ---------------- |
| pushId | String | Yes       | Push task ID |


#### Sample request

```
{
			"pushid":"43214535"
}
```


### Recalling a message (This feature is still being upgraded and not available yet.)

#### API description 

Request method: POST
Request Address
```xml
Service URL/v3/push/revoke_push_msg
```
The API service address corresponds to the service access point one by one; therefore, please select the service address corresponding to your application [service access point](https://www.tencentcloud.com/document/product/1024/38517).

>? Message recall will terminate the offline message delivery of the current push task by default.
>

#### Request parameters

| Parameter | Type | Required | Description |
| ------ | ------ | -------- | ---------------- |
| pushId | String | Yes       | Push task ID |

#### Sample request

```
{
			"pushid":"150032"
}
```

### Message override

#### Step 1. Query the `collapse_id` of the push task

Call the [API for querying push information for one task](https://www.tencentcloud.com/document/product/1024/33773) and get the `collapse_id`, for example, 0001, from the corresponding response parameter.

#### Step 2. Call the push API to override the original push content

When you call the [push API](https://www.tencentcloud.com/document/product/1024/33764), add the `collapse_id`, for example, 0001, obtained in **step 1**. You can also set the `force_collapse` field to decide whether to deliver the message to devices that do not support message override.

>? Message override will terminate the offline message delivery of the original push task by default.
>

#### Sample push
```
{
    "audience_type": "all",
    "collapse_id": 0001,
	  "force_collapse":false,
    "message_type": "notify",
    "message": {
        "title": "Override message 0001",
        "content":"It's a nice day today"		
    },
    "platform": "android"
}
```

### Canceling a scheduled task

#### API description 

Request method: POST
Request Address
```xml
Service URL/v3/push/cancel_timing_task
```
The API service address corresponds to the service access point one by one; therefore, please select the service address corresponding to your application [service access point](https://www.tencentcloud.com/document/product/1024/38517).

>? Cancel a scheduled task that has not yet been scheduled.
>

#### Request parameters

| Parameter | Type | Required | Description |
| ------ | ------ | -------- | ---------------- |
| pushId | String | Yes       | Push task ID |

#### Sample request

```
{
			"pushid":"15003211"
}
```

