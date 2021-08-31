## Use Cases

If a notification message sent by an application contains an error or incorrect redirect link, it will give end users a negative impression of the involved product/service after they view or click it. In this case, you should fix the problem in time. You can choose to terminate, recall, or override the message. This document describes how to do so through the [console](#console) and [RESTful APIs](#restapi).

## Feature Description

- Message termination: terminates all offline messages within the offline storage period of the task.
- Message recall: terminates the current message and makes it disappear from the notification center on devices where it has arrived but has not been clicked. A recall is imperceptible to users.
- Message override: terminates the current message and overrides it with a new one. After a successful override, only the new message will be displayed in the device notification center.

## Use Limits

<table>
<thead>
<tr>
<th>Platform</th>
<th  nowrap="nowrap">Termination</th>
<th>Recall</th>
<th>Override</th>
</tr>
</thead>
<tbody><tr>
<td>Android</td>
<td>Supported</td>
<td>Supported only for the TPNS channel</td>
<td>Supported only for the TPNS channel, Mi channel, Meizu channel, and Huawei devices on EMUI 10 and above</td>
</tr>
<tr>
<td>iOS</td>
<td  nowrap="nowrap">Not supported</td>
<td>Supported    <br> <strong>Notes</strong>:<li>If the application process is manually ended, the message cannot be recalled.<li>Message recall instructions are delivered to devices as silent messages and they have the characteristics of <a href="https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/CreatingtheNotificationPayload.html#//apple_ref/doc/uid/TP40008194-CH10-SW8">silent messages</a>. They will wake up application processes and therefore cause a surge in the number of active applications. You are advised to use the Override feature with priority.</td>
<td>Supported</td>
</tr>
</tbody></table>

>? Message termination, recall, and override are supported only for notifications whose push target is "All devices", "Batch accounts", or "By tags".
>


<span id="console"></span>

## Using the Console

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. Go to **Push Management** > **Task List**.
3. Click **View Details** for the push task to be terminated, overridden, or recalled.
4. In the **Push Progress** column in the top-right corner of the push details page, terminate, override, or recall the task.
![](https://main.qcloudimg.com/raw/f6308cf63712ee5a4feecd47f26d7f31.png)
>? When you select message override, for vivo, OPPO, and Huawei (below EMUI 10) devices that do not support message override, you can choose whether to continue the message delivery:
> - If you choose to continue the delivery, the notification message will be overridden, and both the new and original messages will appear in the device notification center at the same time.
> - If you choose to abort the delivery, no new notification messages will be sent to the above devices that do not support message override.
> 
5. After the operation succeeds, you can return to the **Task List** page and view the current status of the task in the **Status** column.


<span id="restapi"></span>

## Using RESTful APIs

### Message termination

#### API description 

Request method: POST
Request address:
```xml
Service URL/v3/push/stop_push_msg
```

API service URLs correspond to service access points one to one. Please select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

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


### Message recall

#### API description 

Request method: POST
Request address:
```xml
Service URL/v3/push/revoke_push_msg
```
API service URLs correspond to service access points one to one. Please select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

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

Call the [API for querying push information for one task](https://intl.cloud.tencent.com/document/product/1024/33773) and get the `collapse_id`, for example, 0001, from the corresponding response parameter.

#### Step 2. Call the push API to override the original push content

When you call the [push API](https://intl.cloud.tencent.com/document/product/1024/33764), add the `collapse_id`, for example, 0001, obtained in **step 1**. You can also set the `force_collapse` field to specify whether to deliver the message to devices that do not support message override.

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




