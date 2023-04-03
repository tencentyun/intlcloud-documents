## Feature Description

This API is used by the app backend to:

- View responses to friend requests in real time.
- Block malicious responses to friend requests.



## Notes

- To enable this callback, you must configure a callback URL and toggle on the corresponding protocol. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

- An app user initiates a response to accept or reject a friend request.

## Callback Triggering Timing

IM backend receives a response from an app user to a friend request.

>!Responses initiated via RESTful API calls to friend requests will not trigger the callback.

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
| CallbackCommand | Always `Sns.CallbackPrevFriendResponse`                      |
| contenttype     | Always `json`                                                |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
  "CallbackCommand": "Sns.CallbackPrevFriendResponse",
  "Requester_Account": "id",
  "From_Account": "id",
  "ResponseFriendItem": [
    {
      "To_Account": "id1",
      "Remark": "remark1",
      "TagName": "group1",
      "ResponseAction": "Response_Action_AgreeAndAdd"
    },
    {
      "To_Account": "id2",
      "Remark": "remark2",
      "TagName": "group2",
      "ResponseAction": "Response_Action_Reject"
    }
  ],
  "EventTime": 1631777645424
}
```

### Request fields

| Field              | Type    | Description                                                  |
| ------------------ | ------- | ------------------------------------------------------------ |
| CallbackCommand    | String  | Callback command                                             |
| Requester_Account  | String  | `UserID` of the user who initiates the friend request        |
| From_Account       | String  | `UserID` of the user who responds to the friend request      |
| ResponseFriendItem | Array   | Parameter of the response to the friend request              |
| To_Account         | String  | `UserID` of the user who makes the friend request            |
| Remark             | String  | Friend remarks set by `From_Account` for `To_Account`. For more information, see the **Standard friend fields** section in [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521). |
| TagName            | String  | Friend list set by `From_Account` for `To_Account`. For more information, see the **Standard friend fields** section in [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521). |
| ResponseAction     | String  | Response method. Valid values:<br/><li>`Response_Action_AgreeAndAdd`: accept the friend request and add the other party as friend.<br/><li>`Response_Action_Agree`: agree to let the other party add you as friend.<br/><li>`Response_Action_Reject`: reject the friend request. |
| EventTime          | Integer | Timestamp in milliseconds                                    |

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
| To_Account   | String  | Yes      | `UserID` of the user who initiates the friend request        |
| ResultCode   | Integer | Yes      | Result code. Valid values:<br/><li>`0`: allow adding as friend.<br/><li>Other values: do not allow adding as friend.<br/><li>To not allow adding as friend, set the result code to a value in the range of [38000, 39000]. |
| ResultInfo   | String  | Yes      | Error information                                            |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Adding Friends](https://intl.cloud.tencent.com/document/product/1047/34902)
