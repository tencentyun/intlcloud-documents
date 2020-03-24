## Feature Description

This API enables the app backend to promptly monitor (and reject if so configured) group members’ requests to add other users to the group.

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the corresponding callback protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- The callback route is from the IM backend to the app backend, where the IM backend sends HTTP POST requests.
- After receiving a callback request, the app backend must check whether SDKAppID in the request URL is consistent with its own SDKAppID.
- For other security-related matters, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Triggering Scenarios

- An app user sends a request for adding another user to the group through the user’s client.
- The app admin adds the user to the group through this RESTful API.

## Callback Triggering Time

The callback is triggered before the IM backend adds the target user to the group. (If relationship chain hosting exists and the app configures friend relationship verification in IM, this callback will be triggered after the friend relationship is verified as successful.)

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
| CallbackCommand | Its value is fixed to Group.CallbackBeforeInviteJoinGroup. |
| contenttype | Its value is fixed to JSON. |
| ClientIP | The client IP address, for example, 127.0.0.1. |
| OptPlatform | The client platform. For information on the possible values, see the description of the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
 {
    "CallbackCommand": "Group.CallbackBeforeInviteJoinGroup",
    "GroupId": "@TGS#2J4SZEAEL",
    "Type": "Public",
    "Operator_Account": "leckie",
    "DestinationMembers": [
        {
            "Member_Account": "jared"
        },
        {
            "Member_Account": "leckie"
        }
    ]
}
```

### Request packet fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | Callback command |
| GroupId | String | ID of the group to which a user is added |
| Type | String | [Type of the group to be created](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D), for example, Private, Public, or ChatRoom |
| Operator_Account | String | Request operator’s UserID  |
| DestinationMembers | Array | Set of UserID s to be added to the group |

### Response packet example
#### Allowing all users to join a group

The app backend allows all users in requests to join the group.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // Indicates that the system can continue to process requests for adding users to the group.
}
```

#### Rejecting some users to join a group

The app backend rejects some users in requests to join the group and returns these users’ UserID s in RefusedMembers_Account.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "RefusedMembers_Account": [ // List of rejected users
        "jared"
    ]
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. |
| ErrorInfo | String | Required | Error information. |
| RefusedMembers_Account | Array | Optional | The set of rejected users’ IDs. |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [Adding group members](https://intl.cloud.tencent.com/document/product/1047/34921)
