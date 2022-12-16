## Overview
 This API is used by app admins to push system notifications to group chats.

## API Calling Description
### Applicable group types

| Group Type ID | RESTful API Support |
|-----------|------------|
| Private | Yes. Same as the work group (Work) in the new version. |
| Public | Yes |
| ChatRoom | Yes. Same as the meeting group (Meeting) in the new version. |
| AVChatRoom | Yes. But only to all group members.|
| Community | Yes |

These are the preset group types in IM. For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

>?
>- A non-audio-video group supports sending system notifications to specified group members, but an audio-video group (AVChatRoom) only supports sending system notifications to all group members.
>- For more information on the API (`V2TIMGroupListener.onReceiveRESTCustomData`) for clients to receive system notifications, see [Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a0775a137d293473aaed4cf9fc4c18795) or [iOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a34108da2661d1b5ff68d1458ac4dd163).

### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/send_group_system_notification?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https | The request protocol is HTTPS, and the request method is POST. |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<li>China: `console.tim.qq.com`<li>Singapore: `adminapisgp.im.qcloud.com`<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com`<li>Silicon Valley: `adminapiusa.im.qcloud.com`</li> |
| v4/group_open_http_svc/send_group_system_notification | Request API |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format, which should always be `json`.|



### Maximum call frequency

200 calls per second

### Sample request

- **Basic format**
This example pushes a system notification to all members in a group.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "Content": "Hello World" // Content of the notification
}
```

- **To specific members**
To specify who can receive the system notification, set the recipients in `ToMembers_Account`. Audio-video groups (AVChatRoom) only support sending system notifications to all group members, but not specified group members.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "ToMembers_Account": [ // List of recipients. You can leave this field empty to send the notification to all members.
        "peter",
        "leckie"
    ],
    "Content": "Hello World" // Content of the notification
}
```

### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | ID of the group to which the notification will be sent |
| ToMembers_Account | Array | Yes | List of recipients. Up to 500 recipient UserIDs are supported. You can leave this field empty to send the notification to all members. |
| Content | String | Yes | Content of the notification |
| TopicId | String | Optional | The ID of the topic. This option is only avaiable for the community that supports the topic feature.|

### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode | Integer | Error code. `0`: successful; other values: failed |
| ErrorInfo | String | Error information |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | Internal server error. Try again. |
| 10003 | Invalid command word. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007 | No operation permissions. For example, a common member in a public group tries to remove other users from the group, but only the app admin can do so. |
| 10010 | The group does not exist or has been deleted. |
| 10015 | Invalid group ID. Use the correct group ID. |

## API Debugging Tool
Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/group_open_http_svc/send_group_system_notification) to debug this API.

## References
Sending ordinary messages in a group ([v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1047/34959))
