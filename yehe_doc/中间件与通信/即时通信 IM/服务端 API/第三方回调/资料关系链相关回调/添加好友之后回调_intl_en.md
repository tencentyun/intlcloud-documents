## Feature Description

The app backend uses this callback to view information about friends added by users in real time.

## Notes

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

- The app backend uses the RESTful API to initiate a two-way friend addition request, and the peer’s friend request verification mode is "AllowAny".
- The app backend uses the client to initiate a two-way friend addition request, and the peer’s friend verification mode is "AllowAny".
- The app backend uses the RESTful API to initiate a one-way friend addition request.
- The app backend uses the client to initiate a one-way friend addition request.
- After receiving the friend addition request, the app user permits to add the peer as a friend.
- The app backend uses the RESTful API to forcibly add a friend.

## Callback Triggering Time

This callback is triggered when a friend is successfully added.

>!This callback will not be triggered if the API for [importing friends](https://intl.cloud.tencent.com/document/product/1047/34903) is invoked to add a friend.

## API Description
### Request URL example

In the following example, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | The callback URL.                                            |
| SdkAppid        | The SDKAppID assigned by the IM console when an app is created. |
| CallbackCommand | The value is fixed to Sns.CallbackFriendAdd.                 |
| contenttype     | The value is fixed to JSON.                                  |
| ClientIP        | The client IP address, whose format is similar to: 127.0.0.1. |
| OptPlatform     | The client platform. For details on the possible values, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
{
    "CallbackCommand": "Sns.CallbackFriendAdd",
    "PairList": [
        {
            "From_Account": "id",
            "To_Account": "id1",
            "Initiator_Account": "id"
        },
        {
            "From_Account": "id",
            "To_Account": "id2",
            "Initiator_Account": "id"
        },
        {
            "From_Account": "id",
            "To_Account": "id3",
            "Initiator_Account": "id"
        }
    ],
    "ClientCmd":"friend_add",
    "Admin_Account":"",
    "ForceFlag":1
}
```

### Request packet fields

| Field             | Type    | Description                                                  |
| ----------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand   | String  | The callback command.                                        |
| PairList          | Array   | The friend pair that is successfully added.                  |
| From_Account      | String  | From_Account adds To_Account to the friend list.             |
| To_Account        | String  | To_Account is added to the friend list of From_Account.      |
| Initiator_Account | String  | The UserID  of the user who initiates the friend addition request. |
| ClientCmd         | String  | The command keyword that triggers the callback: <br>For a friend addition request, valid values are friend_add and FriendAdd.<br>For a friend addition response, valid values are friend_response and FriendResponse. |
| Admin_Account     | String  | If the current request is a friend addition request triggered by the backend, this field is set to the admin account. Otherwise, this field is empty. |
| ForceFlag         | Integer | The flag for forcibly adding a friend by the admin. 1: the friend is added forcibly. 0: the friend is added as normal. |

### Response packet example

```
{
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "ErrorInfo": ""
}
```

### Response packet fields

| Field        | Type    | Attribute | Description                                                  |
| ------------ | ------- | --------- | ------------------------------------------------------------ |
| ActionStatus | String  | Required  | The request processing result. OK: succeeded. FAIL: failed.  |
| ErrorCode    | Integer | Required  | The error code. 0 indicates that the app backend processing succeeded, and 1 indicates that the app backend processing failed. |
| ErrorInfo    | String  | Required  | Error information.                                           |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [Adding a friend](https://intl.cloud.tencent.com/document/product/1047/34902)
