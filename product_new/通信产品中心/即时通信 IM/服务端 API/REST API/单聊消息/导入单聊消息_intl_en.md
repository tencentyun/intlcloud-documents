## API Description
- This API imports one-to-one chat history to IM.
- It can import your messages from other instant messaging platforms to Tencent Cloud IM.
- This API does not trigger a callback.
- This API deduplicates the imported messages based on the `From_Account`, `To_Account`, `MsgRandom`, and `MsgTimeStamp` fields. **When the values of all the four fields match their counterparts, the two messages are considered duplicates, regardless of their contents.**
- Imported messages will not be overwritten by the same message from later imports.

## API Call Description
### Sample request URL
```
https://console.tim.qq.com/v4/openim/importmsg?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```

### Request parameters
The list below contains only the parameters commonly used when calling this API and their descriptions. For more parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| v4/openim/importmsg | Request API |
| sdkappid | The SDKAppID assigned by the IM console when the application is created. |
| identifier | The administrator account of the app. For more information, see [App Administrator](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | A signature generated in the app administrator account. For details on how to generate the signature, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295. |


### Maximum call frequency

200 calls per second

### Sample request

- **Importing real-time messages**
```
{
    "SyncFromOldSystem": 1, // Imports real-time messages and marks them as unread.
    "From_Account": "lumotuwe1", // The account of the message sender
    "To_Account": "lumotuwe2", // The account of the message recipient
    "MsgRandom": 1287657, // A random number assigned to the message.
    "MsgTimeStamp": 1556178721, // UNIX timestamp in seconds
    "MsgBody": [ // Message body. This is a text message.
        {
            "MsgType": "TIMTextElem", // Message element
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ]
}
```
- **Importing historical messages**
```
 {
    "SyncFromOldSystem": 2, // Imports historical messages and marks them as read.
    "From_Account": "lumotuwe1", // The account of the message sender
    "To_Account": "lumotuwe2", // The account of the message recipient
    "MsgRandom": 1287657, // A random number assigned to the message.
    "MsgTimeStamp": 1556178721, // UNIX timestamp
    "MsgBody": [ // Message body. This is a text message.
        {
            "MsgType": "TIMTextElem", // Message element
            "MsgContent": {
                "Text": "hi, beauty" // Message content.
            }
        }
    ]
}
```


### Request fields

| Field | Type | Required | Description |
|---------|---------|----|---------|
| SyncFromOldSystem | Integer | Yes | Valid values: 1 or 2.<br/>1 means importing real-time messages and marking them as unread.<br/>2 means that importing historical messages and marking them as read. |
| From_Account | String | Yes | The identifier of the message sender|
| To_Account | String | Yes | The identifier of message recipient|
| MsgRandom | Integer | Yes | A number randomly generated and assigned to the message. The backend will use this field to deduplicate messages. For details, refer to the API Description. |
| MsgTimeStamp | Integer | Yes | UNIX timestamp in seconds. It marks the time that the message was sent and is used to deduplicate messages. For details, refer to API Description. |
| MsgBody | Object | Yes | Message body. For detailed information, refer to [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527). Note that MsgBody is an array that can contain multiple message elements. |
| MsgType | String | Yes | TIM message object type. Valid values: TIMTextElem (text), TIMFaceElem (Emoji), TIMLocationElem (location), and TIMCustomElem (custom message) |
| MsgContent | Object | Yes | Different message elements (MsgType) have different `MsgContent` formats. For details, refer to [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527). |



### Sample response

```
{
   "ActionStatus":"OK",
   "ErrorInfo":"",
   "ErrorCode": 0
}

```
### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | The result of the request. `OK` means the request was successful. `FAIL` means the request failed. |
| ErrorCode | Integer | Error code. `0` means the request was successful. Any non-zero value means the request failed. |
| ErrorInfo | String | Detailed error information. |

## Error Codes

Unless a network error (such as error 502) occurs, the returned HTTP status code for this API is always 200. The specific error code and details can be found in the response fields such as `ErrorCode`, and `ErrorInfo`.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).

The list below contains only error codes specific to this API:

| Error Code | Description |
| ------------- | ------------------------------------------------------------ |
| 90001 | Failed to parse the JSON request packet. Make sure the format is valid. |
| 90002 | The format of the MsgBody field in the JSON request packet is invalid or MsgBody is not an array. Refer to [TIMMsgElement Object](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90003 | The To_Account field is missing in the JSON request packet or To_Account is not a string. |
| 90005 | The MsgRandom field is missing in the JSON request packet or MsgRandom is not an integer. |
| 90006 | The MsgTimeStamp field is missing in the JSON request packet or MsgTimeStamp is not an integer. |
| 90007 | The MsgBody field in the JSON request packet is not an array. |
| 90008 | The From_Account field in the JSON request packet i missing or From_Account is not an integer. |
| 90009 | The request requires app administrator permissions. |
| 90010 | Invalid request format. Refer to [TIMMsgElement Object](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement) for more information. |
| 90011 | The number of recipients exceeded 500. Try to reduce the number of accounts in To_Account. |
| 90012 | Accounts in To_Account do not exist or have not been registered. Make sure the accounts are IM accounts and are correct. |
| 90026 | Invalid message offline storage time. Messages cannot be stored offline for more than 7 days. |
| 90030 | The SyncFromOldSystem field is missing in the JSON request packet or SyncFromOldSystem is not an integer. |
| 90048 | The requested account does not exist. |
| 90992 | Internal server error. Please try again. If all requests returned this error code and third-party callback is enabled, make sure the app server is returning the callback results to the IM backend normally. |
| 91000 | Internal server error. Please try again. |
| 93000 | JSON packet exceeded the maximum size of 8 KB. |

## API Debugging Tool
Use the [online RESTful API debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/openim/importmsg) to commission this API.

## See Also
Importing group messages ([v4/group_open_http_svc/import_group_msg ](https://intl.cloud.tencent.com/document/product/1047/34968))
