## Feature Description

Through this callback, the app backend can monitor information about creating groups by users in real time. When the app backend is notified that a group has been created successfully, it performs operations such as data synchronization accordingly.

## Notes

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

- An app user uses a client to successfully create a group.
- The app admin successfully creates a group through the RESTful API.

## Callback Triggering Time

A group has been created successfully.

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
| www.example.com | Callback URL |
| SdkAppid | SDKAppID assigned by the IM console when an app is created |
| CallbackCommand | The value is fixed to Group.CallbackAfterCreateGroup. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, whose format is similar to: 127.0.0.1. |
| OptPlatform | The client platform. For details on the values, see the **OptPlatform** parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
 {
    "CallbackCommand": "Group.CallbackAfterCreateGroup", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",
    "Operator_Account": "group_root", // Operator
    "Owner_Account": "leckie", // Group owner
    "Type": "Public", // Group type
    "Name": "MyFirstGroup", // Group name
    "MemberList": [ // Initial member list
        {
            "Member_Account": "bob"
        },
        {
            "Member_Account": "peter"
        }
    ],
    "UserDefinedDataList": [ //Custom fields during group creation by the user
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

### Request packet fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | The callback command. |
| GroupId | String | The ID of the target group. |
| Operator_Account | String | The UserID  of the operator who initiates the request for creating a group. |
| Owner_Account | String | The UserID  of the owner of the group to be created by the request. |
| Type | String | The type of the group to be created. For details, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D). The group type can be Private, Public, or ChatRoom. |
| Name | String | The name of the group to be created by the request. |
| MemberList | Array | The initial member list of the group to be created by the request. |
| UserDefinedDataList | Array | Custom fields during group creation by the user. By default, this field is unavailable and needs to be enabled before use. For details, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

### Response packet example

After data synchronization, the app backend sends a callback response packet.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // Ignore the callback result
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. 0: ignore the response. |
| ErrorInfo | String | Required | Error information. |

## References
- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [Creating Groups](https://intl.cloud.tencent.com/document/product/1047/34895)
