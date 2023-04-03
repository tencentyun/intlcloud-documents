## Feature Description

This API is used by the app backend to view the recalls of one-to-one messages in real time.

## Notes

- To enable this callback, you must configure the callback URL and enable the corresponding switch for this callback. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTPS POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Trigger Scenarios

- An app user recalls a one-to-one message on the client.
- An app admin recalls a one-to-one message by calling the [admin_msgwithdraw](https://intl.cloud.tencent.com/document/product/1047/35015) API.

## Callback Trigger Timing

After a one-to-one message is recalled successfully

## API Calling Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Sample:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| :-------------- | :----------------------------------------------------------- |
| https           | The request protocol is HTTPS and the request method is POST. |
| www.example.com | Callback URL                                                 |
| SdkAppid        | `SDKAppID` assigned by the IM console when the app is created |
| CallbackCommand | Always `C2C.CallbackAfterMsgWithDraw`                        |
| contenttype     | Always `json`                                                |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
  "CallbackCommand": "C2C.CallbackAfterMsgWithDraw", // Callback command
  "From_Account": "jared", // Sender
  "To_Account": "Jonh", // Recipient
  "MsgKey": "48374_2837546_1557481126", // Unique identifier of the message
  "UnreadMsgNum": 7 // Total number of unread one-to-one messages of `To_Account`
}
```

### Request fields

| Field           | Type    | Description                                                  |
| :-------------- | :------ | :----------------------------------------------------------- |
| CallbackCommand | String  | Callback command                                             |
| From_Account    | String  | `UserID` of the message sender                               |
| To_Account      | String  | `UserID` of the message recipient                            |
| MsgKey          | String  | Unique identifier of the message                             |
| UnreadMsgNum    | Integer | Total number of unread one-to-one messages of `To_Account` (including all one-to-one conversations) |

### Sample response

```
{
  "ActionStatus": "OK",
  "ErrorInfo": "",
  "ErrorCode": 0 // `0`: callback succeeds; `1`: an error occurs during callback.
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| :----------- | :------ | :------- | :----------------------------------------------------------- |
| ActionStatus | String  | Yes      | Request result. `OK`: successful; `FAIL`: failed             |
| ErrorCode    | Integer | Yes      | Error code. `0`: callback succeeds; `1`: an error occurs during callback. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Recalling One-to-One Messages](https://intl.cloud.tencent.com/document/product/1047/35015)
