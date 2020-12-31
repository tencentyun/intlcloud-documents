## Use Cases

If a notification message sent by an application contains an error or wrong redirect link, it will give end users a negative impression of the involved product/service after they view or click it. In this case, you should fix the problem in time. You can choose to terminate, recall, or override the message. This document describes how to do so through the [console](#console) and [RESTful APIs](#restapi).

## Feature Description

- Termination: terminates all offline messages within the offline storage period of the task.
- Recall: terminates the message and makes it disappear from the notification center on devices where it has arrived but has not been clicked. The recall is imperceptible to users.
- Override: terminates the message and overrides it with a new message. After override succeeds, only the new one will be displayed in the device notification center.



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
<td>Supported <br> <strong>Note:</strong> if the application process is manually ended, the message cannot be recalled</td>
<td>Supported</td>
</tr>
</tbody></table>

> ?Message termination/recall/override are only supported for notifications whose push target is "All devices", "Batch accounts", or "By tags".





<span id="console"></span>

## Console Guide

1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns).
2. Select **Push Management** > **Task List** on the left sidebar to enter the task list page and click **View Details** for the push task to be terminated, recalled, or overridden.
3. In the **Push Progress** column in the top-right corner of the push details page, terminate, recall, or override the task.
   ![](https://main.qcloudimg.com/raw/f6308cf63712ee5a4feecd47f26d7f31.png)
> ?When you select message override, for Vivo, OPPO, and Huawei EMUI 10 or below devices that do not support message override, you can choose whether to continue the message delivery:
> - If you choose to continue the delivery, the notification message will be overridden, and both the new and original messages will appear in the device notification center at the same time.
> - If you choose to abort the delivery, no new notification messages will be sent to the above devices that do not support message override.
4. After the operation succeeds, you can return to the **Task List** page and view the current status of the task in the "Status" column.


<span id="restapi"></span>

## RESTful API Guide

### Message termination

#### API description 

Request method: POST
Request address:
```xml
Service address/v3/push/stop_push_msg
```

The API service address corresponds to the service access point one by one; therefore, please select the service address corresponding to your application [service access point](https://intl.cloud.tencent.com/document/product/1024/38517).

#### Request parameters

| Parameter Name | Type | Required | Description |
| ------ | ------ | -------- | ---------------- |
| pushId | string | Yes | Push task ID |


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
Service address/v3/push/revoke_push_msg
```
The API service address corresponds to the service access point one by one; therefore, please select the service address corresponding to your application [service access point](https://intl.cloud.tencent.com/document/product/1024/38517).

>?Message recall will terminate the offline message delivery of the push task by default.

#### Request parameters

| Parameter Name | Type | Required | Description |
| ------ | ------ | -------- | ---------------- |
| pushId | string | Yes | Push task ID |

#### Sample request

```
{
			"pushid":"150032"
}
```

### Message override

#### Step 1. Query the `collapse_id` of the push task

Call the [API for querying push information for one task](https://intl.cloud.tencent.com/document/product/1024/33773) and get the `collapse_id` in the response parameter, such as 0001.

#### Step 2. Call the Push API to override the original push content

When you call the [Push API](https://intl.cloud.tencent.com/document/product/1024/33764), add the `collapse_id` obtained in **step 1** (such as 0001). You can set the `force_collapse` field to decide whether to deliver the message to devices that do not support message override.
>?Message override will terminate the offline message delivery of the original push task by default.

#### Sample push
```
{
    "audience_type": "all",
    "collapse_id": 0001,
	  "force_collapse":false,
    "message_type": "notify",
    "message": {
        "title": "Override message 00001",
        "content":"It's a nice day today"		
    },
    "platform": "android"
}
```




