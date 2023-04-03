## Feature Overview
This webhook event allows you to view the changes in the group profile (group name, group introduction, group notice, and group profile photo) in real time on the app backend. Specifically, you can view the real-time log of the changed group profile or sync the information to other systems.

## Notes

- To enable this webhook, you must configure a webhook URL and toggle on the corresponding protocol. For more information on the configuration method, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this webhook event, the Chat backend initiates an HTTP POST request to the app backend.
- After receiving the webhook request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Webhook Triggering Scenarios

### Webhook triggering content

A group profile includes basic group information and custom group fields. For details, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).
Currently, this webhook may be triggered by a change in the group name, group introduction, group notice, or group profile photo URL, and will not be triggered by a change in other basic group information.

### Webhook triggering methods

- App users modify group profiles through the client.
- App admins modify group profiles through RESTful APIs.

## Webhook Triggering Timing

This webhook is triggered when the basic information of a group is modified.

## API Calling Description

### Sample request URL

In the following sample, the webhook URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Webhook URL                                                  |
| SdkAppid        | The `SDKAppID` assigned by the Chat console when the app is created |
| CallbackCommand | Fixed value: `Group.CallbackAfterGroupInfoChanged`.          |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Webhook Protocols** section of [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackAfterGroupInfoChanged", // Webhook command
    "GroupId" : "@TGS#2J4SZEAEL",
    "Type": "Public", // Group type
    "Operator_Account": "leckie", // Operator
    "Notification": "NewNotification", // New group notice
    "EventTime":"1670574414123"// Event trigger timestamp in milliseconds		
}
```



### Request fields

| Field            | Type    | Description                                                  |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | Webhook command                                              |
| GroupId          | String  | ID of the group whose profile is modified                    |
| Type             | String  | Type of the group whose profile is modified, such as `Public`. For details, see the **Group Types** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |
| Operator_Account | String  | `UserID` of the operator                                     |
| Name             | String  | New group name                                               |
| Introduction     | String  | New group introduction                                       |
| Notification     | String  | New group announcement                                       |
| FaceUrl          | String  | New group profile photo URL                                  |
| EventTime        | Integer | Event trigger timestamp in milliseconds                      |

### Sample response

The application backend records the group profile change information and sends the callback response packet.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // The value `0` indicates that the response result is ignored.
}
```

### Response fields

| Object       | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. `OK`: Successful; `FAIL`: Failed             |
| ErrorCode    | Integer | Yes      | Error code. The value `0` indicates that the response result is ignored. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References

- [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Modifying the Profile of a Group](https://intl.cloud.tencent.com/document/product/1047/34962)
