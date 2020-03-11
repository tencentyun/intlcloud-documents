## Feature Description

Through this callback, the app backend can monitor users’ group creation requests in real time. The backend can reject users’ requests for creating groups.

## Notes

- To enable the callback, you must configure the callback URL and toggle on the callback protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- The callback direction is that the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Introduction: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

- An app user uses a client to create a group.
- The app admin creates a group through the RESTful API.

## Callback Triggering Time

Perform the callback before the IM backend prepares to create a group.

## API Description

### Request URL example

In the following example, the callback URL configured by the app is `https://www.example.com`.
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
| CallbackCommand | The value is fixed to Group.CallbackBeforeCreateGroup. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, such as 127.0.0.1. |
| OptPlatform | The client platform. For information on possible values, see the parameter description for OptPlatform in [Third-Party Callback Introduction: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
{
    "CallbackCommand": "Group.CallbackBeforeCreateGroup", // Callback command
    "Operator_Account": "leckie", // Operator
    "Owner_Account": "leckie", // Group owner
    "Type": "Public", // Group type
    "Name": "MyFirstGroup", // Group name
    "CreatedNum": 123, //Number of groups of the same type already created by the user
    "MemberList": [ // Initial member list
        {
            "Member_Account": "bob"
        },
        {
            "Member_Account": "peter"
        }
    ]
}
```

### Request packet fields

| Field | Type | Feature |
| --- | --- | --- |
| CallbackCommand | String | Callback command |
| Operator_Account | String | Identifier of the operator who initiates the group creation request |
| Owner_Account | String | Identifier of the owner of the group to be created through the request |
| Type | String | The type of the group that generates group messages, such as Private, Public, or ChatRoom. For details, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D). |
| Name | String | Name of the group to be created through the request |
| CreatedNum | Integer | Number of groups of the same type already created by the user |
| MemberList | Array | Initial member list of the group to be created through the request |

### Response packet examples

#### Allowing to create

Allow the user to create the group.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // Allow to create
}
```

#### Rejecting to create

Reject the user’s request to create the group. In this case, the group will not be created, and error code `10016` will be returned to the invoker.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // Reject to create
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. 0: allow creation. 1: reject creation. |
| ErrorInfo | String | Required | The error information. |

## References

- [Third-party callback introduction](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [creating groups](https://intl.cloud.tencent.com/document/product/1047/34895)
