## Feature Description

The app backend can use this callback to monitor users who quit groups in real time, including recording users’ quitting information (for example, recording a log or synchronizing the quitting information to other systems).

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

- An app user quits a group through the client.
- An app user removes a member from a group through the client.
- The app admin removes a member from a group through a RESTful API.

## Callback Triggering Time

The callback is triggered after a user quits a group or is removed from the group by the group owner or admin.

## API Description

### Request URL example

In the following example, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | The callback URL. |
| SdkAppid | The SDKAppID assigned by the IM console when an app is created. |
| CallbackCommand | The value is fixed to Group.CallbackAfterMemberExit. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, whose format is similar to 127.0.0.1. |
| OptPlatform | The client platform. For details on the possible values, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
{
    "CallbackCommand": "Group.CallbackAfterMemberExit", // The callback command.
    "GroupId": "@TGS#2J4SZEAEL", // The group ID.
    "Type": "Public", // The group type.
    "ExitType": "Kicked", // The member quitting method. Possible values are Kicked and Quit.
    "Operator_Account": "leckie", // The operator.
    "ExitMemberList": [ // The list of quit members.
        {
            "Member_Account": "jared"
        },
        {
            "Member_Account": "tommy"
        }
    ]
}
```

### Request packet fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | The callback command. |
| GroupId | String | The ID of the group that generates group messages. |
| Type | String | The type of the group that generates group messages, such as Private, Public, or ChatRoom. For details, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D). |
| ExitType | String | The quitting method of the member. Kicked: the member is removed from the group by the group owner. Quit: the member voluntarily quits the group. |
| Operator_Account | String | The identifier of the member who quits the group. |
| ExitMemberList | Array | The list of quit members. |

### Response packet example

The app backend returns the response packet after synchronizing data.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // The result in the response is ignored.
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. 0: ignore the result in the response. |
| ErrorInfo | String | Required | Error information. |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [Deleting a group member](https://intl.cloud.tencent.com/document/product/1047/34949)
