## Feature Description

The app backend system uses this callback to monitor group member addition messages in real time. This callback can notify the app backend system that new members are added to the group so that the app can perform necessary data synchronization.

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: The IM backend initiates an HTTP POST request to the app backend.
- After receiving a callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

- An app user actively requests to join a group through the client, and the request is approved.
- An app user successfully adds other users to a group through the client.
- An app admin adds users to a group through the RESTful API.

## Callback Triggering Times

- A user actively requests to join a group and successfully joins the group.
- A user is invited by another member to join a group and successfully joins the group.
- An app admin adds the user to a group through the RESTful API.

## API Description

### Request URL example

In the following example, the callback URL configured for the App is `https://www.example.com`.
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
| CallbackCommand | The value is fixed to Group.CallbackAfterNewMemberJoin. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, whose format is similar to: 127.0.0.1. |
| OptPlatform | The client platform. For details on the values, see the **OptPlatform** parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
{
    "CallbackCommand": "Group.CallbackAfterNewMemberJoin", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",
    "Type": "Public", // Group type
    "JoinType": "Apply", // Method for joining a group: Apply (apply to join the group) or Invited (invited to join the group)
    "Operator_Account": "leckie", // Operator member
    "NewMemberList": [ // New member list
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
| GroupId | String | The ID of the group into which other users are to be added. |
| Type | String | The type of the group to be created. For details, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D). The group type can be Private, Public, or ChatRoom. |
| JoinType | String | The method for joining a group: Apply (apply to join the group) or Invited (invited to join the group). |
| Operator_Account | String | The identifier of the request operator. |
| NewMemberList | Array | The list of new members’ identifiers. |

### Response packet example

The app backend system returns the response packet after synchronizing data.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // Ignore the response result
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. The 0 value indicates that the response can be ignored. |
| ErrorInfo | String | Required | Error information. |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [Adding group members](https://intl.cloud.tencent.com/document/product/1047/34921)
