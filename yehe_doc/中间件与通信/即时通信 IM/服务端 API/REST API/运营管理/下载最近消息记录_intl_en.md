## Feature Overview
The app admin can use this API to obtain the download addresses for all one-to-one or group message records in the app that occur at a specified point in time for the last seven days.

>!
>- You can download images, audio, files, and short videos from message records. This feature is only applicable to Chat SDK 4.X or later. The download can be performed based on the URL fields in chat records. If you are using Chat SDK 2.X or 3.X, you cannot obtain the preceding information in this method. If you need this feature, upgrade your Chat SDK to version 4.X or later.
>- Message records are stored as logs and compressed by using GZip. After obtaining the download addresses through the API, you can download and process the message records yourself. Message record files are generated every hour. For example, the data generated at midnight (00:00-00:59) will be processed from 01:00. Typically, the data can be processed within one hour. However, if the message quantity is large, it will take longer to process them. The message record files are valid for only seven days and will be deleted after seven days regardless of the download status. Deleted records cannot be exported again. The download address obtained through this API has an expiration date. Please download the message records before the download address expires. If the download address becomes invalid, obtain the download address again through this API.
>- This API is used only to download historical chat records for the last seven days for backup, statistics, or other purposes. We do not recommend that you use it for real-time online businesses.


## API Calling Description
### Sample request URL
```
https://xxxxxx/v4/open_msg_svc/get_history?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
 ```
### Request parameters
 
The following table describes the modified parameters when this API is called. For other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<br><li>China: `console.tim.qq.com`</li><li>Singapore: `adminapisgp.im.qcloud.com`</li><li>Seoul: `adminapikr.im.qcloud.com`</li><li>Frankfurt: `adminapiger.im.qcloud.com`</li><li>Mumbai: `adminapiind.im.qcloud.com`</li><li>Silicon Valley: `adminapiusa.im.qcloud.com`</li> |
| v4/open_msg_svc/get_history  | Request API                             |
| sdkappid | SDKAppID assigned by the Chat console when an app is created |
| identifier | App admin account. For more information, see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295. |
| contenttype | Request format. The value is fixed to `json`. |

### Maximum call frequency
10 times/second

### Sample request

```
{
    "ChatType": "C2C",
    "MsgTime": "2015120121"
}
```

### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| ChatType | String | Required | Message type. `C2C` indicates a one-to-one message, whereas `Group` indicates a group message. |
| MsgTime | String | Required | Period for downloading message records. For example, 2015120121 indicates that messages in the period of 21:00 to 21:59 on December 1, 2015 will be downloaded. This field needs to be specified by a hour. Each request can only be used to obtain all one-to-one or group message records that occur at the specified hour on the specific day. |

### Sample response
```
{
	"File": [
		{
			"URL": "https://download.tim.qq.com/msg_history/2/9b8f8f063b73f61698ce11e58207e89ade40.gz",
			"ExpireTime": "2015-12-02 16:45:23",
			"FileSize": 65207,
			"FileMD5": "cceece008bb7f469a47cf8c4b7acb84e",
			"GzipSize": 1815,
			"GzipMD5": "c3a0269dde393fd7a8bb18bfdeaeee2e"
		}
	],
	"ActionStatus": "OK",
	"ErrorInfo": "",
	"ErrorCode":0
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | The processing result of the request. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Error code. `0`: Successful; other values: Failed |
| ErrorInfo | String | Error information |
| File | Array  | Download information of the message record file |
| URL | String | Download address of the message record file |
| ExpireTime | String | Expiration time of the download address. Always download the file before the address expires. If the address expires, obtain a new address through the API. |
| FileSize | Integer | File size (in bytes) before GZip compression |
| FileMD5 | String | File MD5 before GZip compression |
| GzipSize | Integer | File size (in bytes) after GZip compression |
| GzipMD5 | String  | File MD5 after GZip compression |

## Error Codes
The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
|---------|---------|
| 1001 | Invalid request. Check whether the request URL is correct. |
| 1002 | Invalid parameter. Check whether the account is the admin, required fields are specified, and the values meet protocol requirements. |
| 1003 | System error. |
| 1004 | The file has not been generated yet, or no message is delivered in the requested period. |
| 1005 | File expired. |

## Format of Message Record Files

```
//For one-to-one messages
{"SdkAppId":1104620500,"ChatType":"C2C","MsgTime":"2015120121","MsgList":[
{"From_Account":"peakerdong","To_Account":"qiyueliuhuo2018","MsgTimestamp":1448974806,"MsgSeq":3452069198,"MsgRandom":45838,"MsgBody":[{"MsgType":"TIMTextElem","MsgContent":{"Text":"Quartering"}}]},
{"From_Account":"group_root","To_Account":"group_test4","MsgTimestamp":1448974808,"MsgSeq":462709847,"MsgRandom":19196437,"MsgBody":[{"MsgType":"TIMTextElem","MsgContent":{"Text":"hi, beauty"}}]}
]}

//For group messages
{"SdkAppId":1104620500,"ChatType":"Group","MsgTime":"2015120121","MsgList":[
{"From_Account":"Test_1","GroupId":"@TGS#1FDFVPAE2","MsgTimestamp":1448975384,"MsgSeq":1,"MsgBody":[{"MsgType":"TIMTextElem","MsgContent":{"Text":"Private activate"}}]},
{"From_Account":"Test_1","GroupId":"@TGS#1FDFVPAE2","MsgTimestamp":1448975384,"MsgSeq":1,"MsgBody":[{"MsgType":"TIMTextElem","MsgContent":{"Text":"Private activate"}}]}
]}
```

The first line of the file records basic information about the file. Each following line records a message until the last line that ends with "]}". For the format of each message, see the definitions in [TIMMsgElement Objects](https://intl.cloud.tencent.com/document/product/1047/33527).
- If the file is small, you can use the JSON database to parse the entire file. `MsgList` indicates the message array for the specified period. For example:
```
# Python sample code
import gzip, json
with gzip.open('1104620500_Group_2015120121.gz', 'rb') as fp:
    info = json.load(fp)
for msg in info['MsgList']:
    pass #do sth with msg
```
- If the file is large, we recommend that you parse it line by line. For example:
```
# Python sample code
import gzip, json
with gzip.open('1104620500_Group_2015120121.gz', 'rb') as fp:
    cnt = -1
    for line in fp:
        line = line.strip().rstrip(b',')
        if line == b']}': break
        if cnt < 0:
            info = json.loads(line + b']}')
        else:
            msg = json.loads(line)
            #do sth with msg
        cnt += 1
```

## API Debugging Tool
Use the [RESTful API online debugging tool](https://tcc.tencentcs.com/im-api-tool/index.html#/v4/open_msg_svc/get_history) to debug this API.

