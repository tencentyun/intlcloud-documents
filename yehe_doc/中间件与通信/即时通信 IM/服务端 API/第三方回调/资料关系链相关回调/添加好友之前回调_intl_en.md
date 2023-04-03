## Feature Description

This API is used by the app backend to:

- View friend requests in real time.
- Block malicious friend requests.



## Notes

- To enable this callback, you must configure a callback URL and toggle on the corresponding protocol. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

- An app user initiates a friend request on the client.

## Callback Triggering Timing

The IM backend receives a friend request from the app.

>!Friend requests initiated via RESTful API calls will not trigger the callback.

## API Calling Description
### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Sample:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS and the request method is POST. |
| www.example.com | Callback URL                                                 |
| SdkAppid        | `SDKAppID` assigned by the IM console when the app is created |
| CallbackCommand | Always `Sns.CallbackPrevFriendAdd`                           |
| contenttype     | Always `json`                                                |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
  "CallbackCommand": "Sns.CallbackPrevFriendAdd",
  "Requester_Account": "id",
  "From_Account": "id",
  "FriendItem": [
    {
      "To_Account": "id1",
      "Remark": "remark1",
      "GroupName": "group1",
      "AddSource": "AddSource_Type_Android",
      "AddWording": "this is id1!"
    },
    {
      "To_Account": "id2",
      "Remark": "remark2",
      "GroupName": "group1",
      "AddSource": "AddSource_Type_Android",
      "AddWording": "this is id2!"
    }
  ],
  "AddType": "Add_Type_Both",
  "ForceAddFlags": 0,
  "EventTime": 1631777344870
}
```

### Request fields

| Field             | Type    | Description                                                  |
| ----------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand   | String  | Callback command                                             |
| Requester_Account | String  | `UserID` of the user who initiates the request               |
| From_Account      | String  | `UserID` of the user who requests to add friend              |
| FriendItem        | Array   | Parameter of the friend request                              |
| To_Account        | String  | `UserID` of user to be added as friend                       |
| Remark            | String  | Friend remarks set by `From_Account` for `To_Account`. For more information, see the **Standard friend fields** section in [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521). |
| GroupName         | String  | Friend list set by `From_Account` for `To_Account`. For more information, see the `Standard friend fields` section in [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521). |
| AddSource         | String  | Source from which a friend is added. For more information, see the `Standard friend fields` section in [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521). |
| AddWording        | String  | Friend request content. For more information, see the `Standard friend fields` section in [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521). |
| AddType           | String  | Friend adding mode. Valid values: <br/><li>`Add_Type_Single`: one-way<br/><li>`Add_Type_Both` (default): two-way |
| ForceAddFlags     | Integer | Flag denoting the friend is force added by an admin. Valid values:<br/><li>`1`: force adding<br/><li>`0`: normal adding |
| EventTime         | Integer | Timestamp in milliseconds                                    |

### Sample response

```
{
  "ActionStatus": "OK",
  "ErrorCode": 0,
  "ErrorInfo": "",
  "ResultItem": [
    {
      "To_Account": "id1",
      "ResultCode": 0,
      "ResultInfo": ""
    },
    {
      "To_Account": "id2",
      "ResultCode": 0,
      "ResultInfo": ""
    }
  ]
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. `OK`: successful; `FAIL`: failed             |
| ErrorCode    | Integer | Yes      | Error code. Valid values:<br/><li>`0`: processing by the app backend is successful.<br/><li>Other values: processing by the app backend fails. The IM backend ignores this error by default.<br/><li>If the processing fails, set the error code to a value in the range of [38000, 39000]. |
| ErrorInfo    | String  | Yes      | Error information                                            |
| ResultItem   | Array   | Yes      | Processing result from the app backend                       |
| To_Account   | String  | Yes      | `UserID` to be added as friend                               |
| ResultCode   | Integer | Yes      | Result code. Valid values:<br/><li>`0`: allow adding as friend.<br/><li>Other values: do not allow adding as friend.<br/><li>To not allow adding as friend, set the result code to a value in the range of [38000, 39000]. |
| ResultInfo   | String  | Yes      | Error information                                            |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Adding Friends](https://intl.cloud.tencent.com/document/product/1047/34902)
