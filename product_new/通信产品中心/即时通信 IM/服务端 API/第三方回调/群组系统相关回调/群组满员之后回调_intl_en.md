## Feature Description

The app backend can use this callback to monitor whether the number of members in a group has reached the limit for the group. This callback can also be used to delete inactive group members to accept new members.

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

- An app user requests to join a group through the client.
- An app user is invited to join a group through the client.
- The app admin adds a member to the group through a RESTful API.

## Callback Triggering Time

The callback is triggered when the number of group members reaches the limit for the group after a new member is added, or when a new member fails to be added to a group because the number of group members has reached the limit.

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
| CallbackCommand | The value is fixed to Group.CallbackAfterGroupFull. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, whose format is similar to 127.0.0.1. |
| OptPlatform | The client platform. For details on the possible values, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
{
    "CallbackCommand": "Group.CallbackAfterGroupFull", // Callback command
    "GroupId": "@TGS#2J4SZEAEL" // Group ID
}
```

### Request packet fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | The callback command. |
| GroupId | String | The ID of the group that is full. |

### Response packet example

After detecting that the number of group members has reached the limit, the app backend sends a callback response packet.

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
- RESTful APIs: [Adding a group member](https://intl.cloud.tencent.com/document/product/1047/34921)
