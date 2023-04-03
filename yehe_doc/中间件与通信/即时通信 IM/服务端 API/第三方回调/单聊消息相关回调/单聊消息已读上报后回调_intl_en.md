- ## Feature Description

  This API is used by the app backend to view one-to-one message reads in real time.

  ## Notes

  - To enable this callback, you must configure the callback URL and enable the corresponding switch for this callback. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
  - During this callback, the IM backend initiates an HTTPS POST request to the app backend.
  - After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
  - For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

  ## Callback Trigger Scenarios

  - An app user marks a one-to-one message as read on the client.
  - An app admin marks a one-to-one message as read by calling the [admin_set_msg_read](https://intl.cloud.tencent.com/document/product/1047/38996) API.

  ## Callback Trigger Timing

  After a one-to-one message is marked as read

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
  | CallbackCommand | Always `C2C.CallbackAfterMsgReport`                          |
  | contenttype     | Always `json`                                                |
  | ClientIP        | Client IP, such as 127.0.0.1                                 |
  | OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

  ### Sample request

  ```
  {
    "CallbackCommand": "C2C.CallbackAfterMsgReport", // Callback command
    "Report_Account": "jared", // Read reporter
    "Peer_Account": "Jonh", // The other party in the conversation
    "LastReadTime": 1614754606, // Read time
    "UnreadMsgNum": 7 // Total number of unread one-to-one messages of `Report_Account`
  }
  ```

  ### Request fields

  | Field           | Type    | Description                                                  |
  | :-------------- | :------ | :----------------------------------------------------------- |
  | CallbackCommand | String  | Callback command                                             |
  | Report_Account  | String  | `UserID` of the read reporter                                |
  | Peer_Account    | String  | `UserID` of the other party in the conversation              |
  | LastReadTime    | Integer | Read time                                                    |
  | UnreadMsgNum    | Integer | Total number of unread one-to-one messages of `Report_Account` (including all one-to-one conversations) |

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
  - [Marking One-to-One Messages as Read](https://intl.cloud.tencent.com/document/product/1047/38996)
