## Feature Description
This API is used to query the unread message count of a one-to-one conversation or all one-to-one conversations.

## API Calling Description

### Sample request URL

```
https://xxxxxx/v4/openim/get_c2c_unread_msg_num?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```

### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/openim/get_c2c_unread_msg_num  | Request API |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |

### Maximum calling frequency

200 calls per second

### Querying the total unread one-to-one message count of an account

#### Sample request

This example shows how the admin queries the total unread one-to-one message count of `dramon1`. Only `To_Account` is required.

```
{
    "To_Account":"dramon1"
}
```

#### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "AllC2CUnreadMsgNum": 12
}
```

### Querying the unread message counts of multiple one-to-one conversations at a time

#### Sample request

This example shows how the admin queries the unread message counts of `dramon1`'s conversations with `dramon2` and `teacher`.

```
{
    "To_Account":"dramon1",
    "Peer_Account":[
        "dramon2",
        "teacher"
    ]
}
```

#### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "C2CUnreadMsgNumList": [
        {
            "Peer_Account": "dramon2",
            "C2CUnreadMsgNum": 12
        },
        {
            "Peer_Account": "teacher",
            "C2CUnreadMsgNum": 12
        }
    ]
}
```

### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| To_Account | String | Yes | `UserID` of the user to query |
| Peer_Account | Array | No | `UserID` of the other party in the conversation to query <li>This field is required to query a specific one-to-one conversation. </li><li>The array can contain up to 10 `UserID` values.</li>|

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode| Integer | Error code. `0`: successful; other values: failed |
| ErrorInfo | String | Error information |
| AllC2CUnreadMsgNum | Integer | Total unread message count of all conversations |
| C2CUnreadMsgNumList.Peer_Account | String | `UserID` of the other party in the one-to-one conversation  |
| C2CUnreadMsgNumList.C2CUnreadMsgNum| Integer | Unread message count in the one-to-one conversation  |
| ErrorList.Peer_Account | String | Target account for which the query failed  |
| ErrorList.ErrorCode| Integer | Error code. `70107` indicates that the account does not exist. |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------------- | ------------------------------------------------------------ |
| 90001 | Failed to parse the JSON request. Make sure the format is valid. |
| 90003 | The `To_Account` field is missing in the JSON request or the account it specifies does not exist. |
| 90008 | The `From_Account` field is missing in the JSON request or the account it specifies does not exist. |

## References
- Sending One-to-One Messages to One User ([v4/openim/sendmsg](https://intl.cloud.tencent.com/document/product/1047/34919))
- Sending One-to-One Messages to Multiple Users ([v4/openim/batchsendmsg](https://intl.cloud.tencent.com/document/product/1047/34920))
- Querying One-to-One Messages ([v4/openim/admin_getroammsg](https://intl.cloud.tencent.com/document/product/1047/35478))
- Recalling One-to-One Messages ([v4/openim/admin_msgwithdraw](https://intl.cloud.tencent.com/document/product/1047/35015))
