## Feature Description
- This API imports one-to-one chat history to IM.
- It imports your messages from other instant messaging platforms to Tencent Cloud IM.
- It does not trigger a callback.
- It deduplicates the imported messages based on the `From_Account`, `To_Account`, `MsgRandom`, and `MsgTimeStamp` fields. **When the values of all the four fields match their counterparts, the two messages are considered duplicates, regardless of their contents.**
- Imported messages will not be overwritten by the same messages from later imports.

## API Calling Description
### Sample request URL
```
https://console.tim.qq.com/v4/openim/importmsg?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```

### Request parameters
The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| v4/openim/importmsg | Request API |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |


### Maximum calling frequency

200 calls per second

### Sample requests

- **Importing real-time messages**
```
{
    "SyncFromOldSystem": 1, // Imports real-time messages and marks them as unread.
    "From_Account": "lumotuwe1", // Account of the sender
    "To_Account": "lumotuwe2", // Account of the recipient
    "MsgRandom": 1287657, // Random number of the message
    "MsgTimeStamp": 1556178721, // UNIX timestamp in seconds
    "MsgBody": [ // Message body. This is a text message.
        {
            "MsgType": "TIMTextElem", // Text message element
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```
- **Importing historical messages**
```
 {
    "SyncFromOldSystem": 2, // Imports historical messages and marks them as read.
    "From_Account": "lumotuwe1", // Account of the sender
    "To_Account": "lumotuwe2", // Account of the recipient
    "MsgRandom": 1287657, // Random number of the message
    "MsgTimeStamp": 1556178721, // UNIX timestamp in seconds
    "MsgBody": [ // Message body. This is a text message.
        {
            "MsgType": "TIMTextElem", // Text message element
            "MsgContent": {
                "Text": "hi, beauty" // Message content
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```


### Request fields

| Field | Type | Required | Description |
|---------|---------|----|---------|
| SyncFromOldSystem | Integer | Yes | Valid values: `1`, `2`<br/>`1`: imports real-time messages and marks them as unread.<br/>`2`: imports historical messages and marks them as read. |
| From_Account | String | Yes | `UserID` of the sender, which is used to specify the message sender |
| To_Account | String | Yes | `UserID` of the recipient |
| MsgRandom | Integer | Yes | A number randomly generated and assigned to the message. The backend will use this field to deduplicate messages. For details, see **Feature Description**. |
| MsgTimeStamp | Integer | Yes | UNIX timestamp in seconds. It marks the time when the message was sent and is used to deduplicate messages. For details, see **Feature Description**. |
| MsgBody | Object | Yes | Message body. For details on formats, please see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). (Note: a message can contain multiple message elements, in which case `MsgBody` is an array.) |
| MsgType | String | Yes | TIM message object type. Valid values: <ul style="margin:0;"><li >`TIMTextElem` (text message) <li >`TIMLocationElem` (location message) <li >`TIMFaceElem` (emoji message) <li >`TIMCustomElem` (custom message) <li >`TIMSoundElem` (voice message) <li >`TIMImageElem` (image message) <li >`TIMFileElem` (file message) <li >`TIMVideoFileElem` (video message) |
| MsgContent | Object | Yes | Different message object types (`MsgType`) have different formats (`MsgContent`). For details, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| CloudCustomData | String | No | Custom message data. It is saved in the cloud and will be sent to the peer end. Such data can be pulled after the app is uninstalled and reinstalled. |



### Sample response

```
{
   "ActionStatus" : "OK",
   "ErrorInfo" : "",
   "ErrorCode" : 0
}

```
### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode | Integer | Error code. `0`: successful; other values: failed |
| ErrorInfo | String | Error information |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).

The following table describes the error codes specific to this API:

| Error Code | Description |
| ------------- | ------------------------------------------------------------ |
| 90001 | Failed to parse the JSON request. Make sure the format is valid. |
| 90002 | The `MsgBody` in the JSON request does not meet message format requirements or it is not an array. For more information, see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90003 | The `To_Account` field is missing in the JSON request or it is not a string. |
| 90005 | The `MsgRandom` field is missing in the JSON request or it is not an integer. |
| 90006 | The `MsgTimeStamp` field is missing in the JSON request or it is not an integer. |
| 90007 | The `MsgBody` field in the JSON request is not an array. Change it to an array. |
| 90008 | The `From_Account` field is missing in the JSON request or it is not an integer. |
| 90009 | The request requires app admin permissions. |
| 90010 | The JSON request does not meet message format requirements. For more information, see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90011 | The number of target accounts exceeds 500. Delete some `To_Account`. |
| 90012 | The account specified in `To_Account` does not exist or is not registered. Make sure the account has been imported to IM and is correct. |
| 90026 | Invalid message offline storage time. Messages cannot be stored offline for more than 7 days. |
| 90030 | The `SyncFromOldSystem` field is missing in the JSON request or it is not an integer. |
| 90048 | The requested account does not exist. |
| 90992 | Internal service error. Try again. If this error code is returned for all requests and third-party callback is enabled, make sure the app server returns the callback results to the IM backend normally. |
| 91000 | Internal service error. Try again. |
| 93000 | The JSON packet exceeds the maximum size of 8 KB. |

## API Debugging Tool
Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/openim/importmsg) to debug this API.

## Reference
Importing Group Messages ([v4/group_open_http_svc/import_group_msg](https://intl.cloud.tencent.com/document/product/1047/34968))
