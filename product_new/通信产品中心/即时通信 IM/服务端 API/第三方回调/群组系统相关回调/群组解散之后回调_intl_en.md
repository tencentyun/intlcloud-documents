## Feature Description

The app backend uses this callback to monitor group dismissal in real time, including recording group dismissal information in real time (for example, recording a log or synchronizing the information to other systems).

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

- An app user dismisses a group through a client.
- The app admin dismisses a group through a RESTful API.

## Callback Triggering Time

The callback is triggered after a group is dismissed.

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
| CallbackCommand | The value is fixed to Group.CallbackAfterGroupDestroyed. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, whose format is similar to 127.0.0.1. |
| OptPlatform | The client platform. For details on the possible values, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
{
    "CallbackCommand": "Group.CallbackAfterGroupDestroyed", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",
    "Type": "Public", // Group type
    "Owner_Account": "leckie", // Group owner
    "Name": "MyFirstGroup", // Group name
    "MemberList" : [ // Members in the dismissed group
        {
            "Member_Account": "leckie"
        },
        {
            "Member_Account": "peter"
        },
        {
            "Member_Account": "bob"
        }
    ]
}
```

### Request packet fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | The callback command. |
| GroupId | String | The ID of the dismissed group. |
| Type | String | The type of the dismissed group, such as Private, Public, or ChatRoom. For details, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D). |
| Owner_Account | String | The UserID  of the group owner. |
| MemberList | Array | The member list of the dismissed group. |

### Response packet example

After recording group dismissal information, the app backend sends a callback response packet.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. We recommend that you set this field to 0. This callback is used to notify users after the group is dismissed. The error code value does not affect the normal group dismissal process. |
| ErrorInfo | String | Required | Error information. |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [Dismissing groups](https://intl.cloud.tencent.com/document/product/1047/34896)
