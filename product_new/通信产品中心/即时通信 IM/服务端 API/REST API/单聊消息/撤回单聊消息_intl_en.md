## API Description
- This API lets administrators recall one-to-one messages.
- This API can recall all one-to-one messages, including those sent by the client or by the [Sending a One-to-one Message](https://intl.cloud.tencent.com/document/product/1047/34919) and [Batch Sending One-to-one Messages](https://intl.cloud.tencent.com/document/product/1047/34920) APIs.
- You need to enable [Callback before Sending One-to-one messages](https://intl.cloud.tencent.com/document/product/269/1632) or [Callback before Sending One-to-one messages](https://intl.cloud.tencent.com/document/product/269/2716) before you are able to recall one-to-one messages sent by the client. These APIs record the `MsgKey` of each message, which is used as a field of this API to recall messages.
- Use the `MsgKey` fields in the responses to messages sent by the [Sending a One-to-one Message](https://intl.cloud.tencent.com/document/product/1047/34919) and [Batch Sending One-to-one Messages](https://intl.cloud.tencent.com/document/product/1047/34920) APIs to recall these one-to-one messages.
- Once a one-to-one message is recalled using this API, it is recalled from offline storage, roaming storage, and the client’s local cache.
- This API can recall one-to-one messages sent at any time. There’s no time limit.

> Exercise caution when using this API. One-to-one messages recalled by this API cannot be restored.

## Input Parameters
### Sample request URL
```
https://console.tim.qq.com/v4/openim/admin_msgwithdraw?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Parameters

The following is a list of the parameters commonly used when calling this API and their descriptions. For more parameters, see the [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| v4/openim/admin_msgwithdraw | Request API |
| sdkappid | The SDKAppID is assigned by the IM console when the app is created. |
| identifier  | The administrator account of the app. For more information, refer to [App Administrator](https://cloud.tencent.com/document/product/269/31999#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | A signature generated from the app administrator account. For details on how to generate the signature, refer to [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-digit integer ranging from 0 to 4294967295. |

### Maximum calling frequency

200/second

### Sample request
```
{
	"From_Account": "vinson",
	"To_Account": "dramon",
	"MsgKey": "31906_833502_1572869830"
}
```


### Request field descriptions

| Field | Type | Required | Description |
|---------|---------|----|---------|
| From_Account | String | Yes | UserID of the message sender  |
| To_Account | String | Yes | UserID of the recipient  |
| MsgKey | String | Yes | Unique identifier of the message, which is found in the responses to messages sent by the [Sending a One-to-one Message](https://intl.cloud.tencent.com/document/product/1047/34919) and [Batch Sending One-to-one Messages](https://intl.cloud.tencent.com/document/product/1047/34920) APIs |



### Sample response
- Response to a successful recall
```
{
    "ActionStatus":"OK", 
    "ErrorInfo":"", 
    "ErrorCode": 0
}
```
- Response to a failed recall
```
{
    "ActionStatus": "FAIL", 
    "ErrorInfo": "Fail to Parse json data of body, Please check it", 
    "ErrorCode": 90001
}
```

### Response field descriptions

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Status of the operation. `OK` means the request was successful. `FAIL` means the request failed. |
| ErrorCode| Integer | Error code. `0` means the operation was successful. Any non-zero value means the request failed. |
| ErrorInfo| String | Detailed error information. |

## Error Codes

An HTTP status code 200 means the request was successfully received. The result of the blacklist operation is in the response, with details provided in fields such as `ErrorCode` and `ErrorInfo`. An HTTP status other than 200, such as 502, means the request was not received.
For public error codes (60000 to 79999), refer to [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following are error codes specific to this API:

| Error Code | Description |
| ------------- | ------------------------------------------------------------ |
| 90001 | Failed to parse JSON. Make sure the format is valid. |
| 90003 | There is no `To_Account` or the account it specifies does not exist. |
| 90008 | There is no `From_Account` or the account it specifies does not exist. |
| 90009 | The request requires app administrator permissions. |
| 90054 | Invalid `MsgKey`. |
| 91000 | Internal server error. Please try again. |


## See Also
- Sending a one-to-one message ([v4/openim/sendmsg](https://intl.cloud.tencent.com/document/product/1047/34919))
- Batch sending one-to-one messages ([v4/openim/batchsendmsg](https://cloud.tencent.com/document/product/269/1612))


