## Overview

This API is used by the app backend to monitor the recalls of group messages in real time.

## Notes

- To enable this callback, you must configure a callback URL and enable the corresponding switch for this callback. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Trigger Scenarios

- An app user recalls a group message on the client.
- An app admin recalls a group message via calling the RESTful API.

## Callback Trigger Timing

After a group message is recalled successfully

## API Calling Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Sample:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Callback URL |
| SdkAppid | The `SDKAppID` assigned by the IM console when the app is created |
| CallbackCommand | The value is always `Group.CallbackAfterRecallMsg`. |
| contenttype | The value is always `JSON`. |
| ClientIP | Client IP, such as 127.0.0.1 |
| OptPlatform | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand":"Group.CallbackAfterRecallMsg", // Callback command
    "Operator_Account":"admin", // Operator
    "Type": "Public", // Group type
    "GroupId":"1213456", // Group ID
    "MsgSeqList":[ // `MsgSeq` list of recalled messages           
        {"MsgSeq":130}
    ]
}
```

### Request fields

| Object | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | Callback command |
| Operator_Account | String | The `UserID` of the operator who recalls a group message |
| Type | String | Type of the group that generates group messages, such as `Public`. For details, see **Group Types** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |
| GroupId | String | Group ID |
| MsgSeqList | Array | `MsgSeq` list of recalled messages |

### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorInfo":"",
    "ErrorCode": 0 //The value `0` indicates that the callback result is ignored.
}
```

### Response fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Yes | Request result. `OK`: Successful; `FAIL`: Failed |
| ErrorCode | Integer | Yes | Error code. The value `0` indicates that the callback result is ignored. |
| ErrorInfo | String | Yes | Error information |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- Restful API: [Recalling Group Messages](https://intl.cloud.tencent.com/document/product/1047/34965)


