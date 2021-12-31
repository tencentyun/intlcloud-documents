## Feature Description
This API is used to pull a conversation list by page.

## API Calling Description
### Sample request URL
```
https://xxxxxx/v4/recentcontact/get_list?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https | The request protocol is HTTPS, and the request method is POST. |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<li>China: `console.tim.qq.com`<li>Singapore: `adminapisgp.im.qcloud.com`<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/recentcontact/get_list  | Request API                             |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |

### Maximum call frequency

200 calls per second

### Sample request
```
{
  "From_Account": "id1",
  "TimeStamp": 0,
  "StartIndex": 0,
  "TopTimeStamp": 0,
  "TopStartIndex": 0,
  "AssistFlags": 7
}
```

### Request fields

|Field|Type|Required|Description|
|-------|------|-------|-----|
|From_Account|String|Yes |`UserID` of the account for which to pull a conversation list|
|TimeStamp|Integer|Yes |Start time of general conversations. Enter `0` for the first page. |
|StartIndex|Integer|Yes|Starting point of general conversations. Enter `0` for the first page. |
|TopTimeStamp| Integer | Yes |Start time of pinned conversations. Enter `0` for the first page. |
|TopStartIndex| Integer | Yes |Starting point of pinned conversations. Enter `0` for the first page. |
|AssistFlags|Integer| Yes | Flag bits of conversations:<br/>    Bit 0: whether to support pinned conversations<br/>    Bit 1: whether to return an empty conversation<br/>    Bit 2: whether to support paginating pinned conversations |

### Sample response

```
{
  "SessionItem": [
    {
      "Type": 1,
      "To_Account": "id2",
      "MsgTime": 1630997627,
      "TopFlag": 1
    },
    {
      "Type": 2,
      "GroupId": "id3",
      "MsgTime": 1630997628,
      "TopFlag": 1
    },
    {
      "Type": 1,
      "To_Account": "id4",
      "MsgTime": 1630997630,
      "TopFlag": 0
    },
    {
      "Type": 2,
      "GroupId": "id5",
      "MsgTime": 1630997650,
      "TopFlag": 0
    }
  ],
  "CompleteFlag": 1,
  "TimeStamp": 1631012800,
  "StartIndex": 0,
  "TopTimeStamp": 1631012800,
  "TopStartIndex": 0,
  "ActionStatus": "OK",
  "ErrorCode": 0,
  "ErrorInfo": "",
  "ErrorDisplay": ""
}
```


### Response fields

|Field|Type|Description|
|------|------|-------|
| SessionItem |Array| Array of conversation objects |
| Type | Integer | Conversation type. `1`: one-to-one conversation; `2`: group conversation |
| To_Account | String | `UserID` of the other conversation participant, which will be returned only for a one-to-one conversation |
| GroupId | String | Group ID, which will be returned only for a group conversation |
| MsgTime | Integer | Conversation duration |
| TopFlag | Integer | Flag of conversation pinning. `0`: general conversation; `1`: pinned conversation |
| CompleteFlag | Integer | Completion flag. `1`: all conversation are returned; `0`: pulling has not finished yet. |
| TimeStamp | Integer | Start time of the next pulled page for a general conversation, which is sent to the IM backend via the `TimeStamp` field of the request during pulling-by-page |
| StartIndex | Integer | Starting point of the next pulled page for a general conversation, which is sent to the IM backend via the `StartIndex` field of the request during pulling-by-page |
| TopTimeStamp | Integer | Start time of the next pulled page for a pinned conversation, which is sent to the IM backend via the `TopTimeStamp` field of the request during pulling-by-page |
| TopStartIndex | Integer | Starting point of the next pulled page for a pinned conversation, which is sent to the IM backend via the `TopStartIndex` field of the request during pulling-by-page |
| ActionStatus | String | The request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode | Integer | Error code. `0`: successful; other values: failed. For details on non-zero results, please see [Error Codes](#ErrorCode). |
| ErrorInfo | String | Error information |
| ErrorDisplay | String | Detailed information displayed on the client |

[](id:ErrorCode)
## Error Codes
The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ResultCode`, `ResultInfo`, `ErrorCode`, and `ErrorInfo`.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 50001  | The requested UserID has not been imported into the Tencent Cloud IM backend. Please import. |
| 50002  | Incorrect request parameter. Check your request according to the error description.                                    |
| 50003  | The request requires app admin permissions.                                      |
| 50004  | Internal server error. Please try again.                                      |
| 50005  | Network timeout. Try again later.                                       |

## API Debugging Tool
Use our [RESTful API Tester](https://avc.cloud.tencent.com/im/APITester/APITester.html#v4/recentcontact/get_list) to test your requests.
