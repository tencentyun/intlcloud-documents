## Feature Overview

This callback allows you to view the information of the topic created by the user on the application backend in real time. Specifically, it notifies the application backend of the successful topic creation so that the backend can sync data.

## Notes

- To enable this callback, you must configure the URL. This callback and the callback after group creation use the same switch. For detailed directions, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).
- You need to [enable the topic feature in the console](https://intl.cloud.tencent.com/document/product/1047/34419) before using it.

## Callback Triggering Scenarios

- The application user created a topic successfully on the client.
- The application admin created a topic successfully through the RESTful API.

## Callback Triggering Timing

It will be triggered after a topic is created successfully.

## API Calling Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Callback URL                                                 |
| SdkAppid        | The `SDKAppID` assigned by the IM console when the app is created |
| CallbackCommand | Fixed value: `Group.CallbackAfterCreateTopic`.               |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```json
 {
    "CallbackCommand": "Group.CallbackAfterCreateTopic", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",
    "TopicId"	: "@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_@TOPIC#cRTE3HIM62C5",
    "Operator_Account": "group_root", // Operator
    "Owner_Account": "leckie", // Group owner
    "Type": "Community", // Group type
    "Name": "MyFirstTopic", // Topic name
    "UserDefinedDataList": [ // Custom field to be used when the user creates a topic
        {
            "Key": "UserDefined1",
            "Value": "hello"
        },
        {
            "Key": "UserDefined2",
            "Value": "world"
        }
    ]
}
```

### Request fields

| Field               | Type   | Description                                                  |
| ------------------- | ------ | ------------------------------------------------------------ |
| CallbackCommand     | String | Callback command                                             |
| GroupId             | String | Group ID of the topic                                        |
| TopicId             | string | Topic ID                                                     |
| Operator_Account    | String | `UserID` of the operator who initiates the topic creation request |
| Owner_Account       | String | `UserID` of the group owner                                  |
| Type                | String | Group type of the topic. Here, it is `Community`.            |
| Name                | String | Name of the topic requested to be created                    |
| UserDefinedDataList | Array  | Custom field to be used when the user creates a topic. This field is unavailable by default and needs to be enabled as instructed in [Group System](https://www.tencentcloud.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### Sample response

A response is sent after the app backend synchronizes the data.

```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 //The value `0` indicates that the callback result is ignored.
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. `OK`: Successful; `FAIL`: Failed             |
| ErrorCode    | Integer | Yes      | Error code. The value `0` indicates that the callback result is ignored. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References
- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Creating Topic](https://intl.cloud.tencent.com/document/product/1047/49471)
