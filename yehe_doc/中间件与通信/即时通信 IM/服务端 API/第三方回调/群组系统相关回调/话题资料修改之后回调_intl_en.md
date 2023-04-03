## Feature Overview
This callback allows you to view the changes in the topic profile (topic name, topic introduction, topic notice, and topic profile photo) in real time on the application backend. Specifically, you can view the real-time log of the changed topic profile or sync the information to other systems.

## Notes

- To enable this callback, you must configure the URL. This callback and the callback after group profile modification use the same switch. For detailed directions, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).
- You need to [enable the topic feature in the console](https://intl.cloud.tencent.com/document/product/1047/34419) before using it.

## Callback Triggering Scenarios

### Callback triggering content

The topic profile includes the basic topic profile and custom topic field.
Currently, this callback may be triggered by a change in the topic name, topic introduction, topic notice, or topic profile photo URL, and will not be triggered by a change in other basic topic profile.

### Callback triggering methods

- The app user modifies the topic profile on the client.
- The app admin modifies the topic profile through the RESTful API.

## Callback Triggering Timing

It will be triggered after the topic profile is changed.

## API Calling Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```json
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Callback URL                                                 |
| SdkAppid        | The `SDKAppID` assigned by the IM console when the app is created |
| CallbackCommand | Fixed value: `Group.CallbackAfterTopicInfoChanged`.          |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```json
{
    "CallbackCommand": "Group.CallbackAfterTopicInfoChanged", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",	// Group ID of the changed topic profile
    "Type": "Community", // Group type
    "Operator_Account": "leckie", // Operator
    "Name":	"TestTopic", // Changed topic name
    "Introduction": "TestIntroduction", // Changed topic introduction
    "Notification": "NewNotification", // Changed topic notice
    "FaceUrl": "http://this.is.face.url"	// Changed topic profile photo URL
}
```

### Request fields

| Field            | Type   | Description                                               |
| ---------------- | ------ | --------------------------------------------------------- |
| CallbackCommand  | String | Callback command                                          |
| GroupId          | String | Group ID of the changed topic profile                     |
| Type             | String | Group type of the deleted topic. Here, it is `Community`. |
| Operator_Account | String | `UserID` of the operator                                  |
| Name             | String | Changed topic name                                        |
| Introduction     | String | Changed topic introduction                                |
| Notification     | String | Changed topic notice                                      |
| FaceUrl          | String | Changed topic profile photo URL                           |

### Sample response

The application backend records the topic profile change information and sends the callback response packet.

```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0  // Ignore the response result
}
```

### Response fields

| Object       | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. Valid values: `OK` (success); `FAIL`: (failure). |
| ErrorCode    | Integer | Yes      | Error code. The value `0` indicates to allow ignoring the response result. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Modifying Topic Profile](https://intl.cloud.tencent.com/document/product/1047/49468)
