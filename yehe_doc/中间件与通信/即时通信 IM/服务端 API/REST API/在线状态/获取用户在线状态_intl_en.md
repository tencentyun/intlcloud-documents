## Feature Description
This API is used to query the current login status of a user.

## API Call Description
### Sample request URL
```
https://xxxxxx/v4/openim/querystate?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The following table lists and describes only the parameters to be modified when this API is called. For more parameters, see [REST API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/openim/querystate | Request API. |
| sdkappid | The SDKAppID assigned by the Instant Messaging (IM) console when the application is created. |
| identifier | The value must be the administrator account of the app. For more information, see [App Administrator](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated for the administrator account of the app. For more information about the operation, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | The value can be a random 32-bit unsigned integer. Value range: 0 to 4294967295. |
| contenttype | Request format. The value is always `json`. |

### Maximum call frequency

This API can be called up to 200 times per second.

### Sample request packet
#### When detailed login platform information is not needed
```
{
    "To_Account": ["id1", "id2", "id3"]
}

```

#### When detailed login platform information is needed
```
{
    "IsNeedDetail": 1,
    "To_Account": ["id1", "id2"]
}
```

### Description of fields in a request packet

| Field | Type | Required | Description |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| To_Account | Array | Required | The one or more UserIDs whose login statuses are to be queried. This API can be used to query the login statuses of up to 500 UserIDs at a time. |
| IsNeedDetail | Integer | Optional | Specifies whether detailed login platform information is needed in the response. 0: Not needed; 1: Needed. |

### Sample response packet body
#### When detailed login platform information is not needed

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "QueryResult": [
        {
            "To_Account": "id1",
            "State": "Offline"
        },
        {
            "To_Account": "id2",
            "State": "Online"
        },
        {
            "To_Account": "id3",
            "State": "PushOnline"
        }
    ]
}

```
#### When detailed login platform information is needed
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "QueryResult": [
        {
            "To_Account": "id1",
            "State": "Online",
            "Detail": [
                {
                    "Platform": "IPhone",
                    "Status": "PushOnline"
                },
                {
                    "Platform": "Web",
                    "Status": "Online"
                }
            ]
        },
        {
            "To_Account": "id2",
            "State": "Offline",
        }        
    ]
}
```

#### Request error
```
{
    "ActionStatus": "FAIL",
    "ErrorInfo": "Fail to Parse json data of body, Please check it",
    "ErrorCode": 90001
}
```

### Description of fields in a response packet

| Field | Type | Description |
| ------------ | ------- | ------------------------------------------------------------ |
| ActionStatus | String | Processing result of the request. OK: successful; FAIL: failed. |
| ErrorCode | Integer | Error code. Valid values: 0: successful; Non-zero: failed. |
| ErrorInfo | String | Detailed information about the error. |
| QueryResult | Array | The returned structured information of the login status of the user. |
| To_Account | String | The returned UserID of the user whose login status is queried. |
| State | String | The returned login status. Valid values: <ul style="margin:0;"><li>Online: after the user logs in to the client, the client remains in a persistent connection with the IM console.</li><li>PushOnline: the client enters the PushOnline state when the iOS or Android process is disconnected due to a network error or is terminated by the operating system. In this state, the client still can receive offline messages. However, if the client’s process is not terminated by the operating system after the client is switched to the background, the client is in Online state.</li><li>Offline: the user logs out of the client properly or has not logged in to the client for at least 7 days since the last login.</li></ul>If the user logs in to the client on multiple devices, the field is Online provided that the client is in the Online state on any device. |
| Detail | Object | Detailed login platform information. |
| Platform | String | The type of the login platform. |
| Status | String | The status of the login platform. |

>! The IM backend stores the PushOnline status for only 7 days. If a user has not logged in to the client for 7 days since disconnection, the client enters the Offline status.

## Error Codes
The HTTP return code for this API is 200 unless an network error such as error 502 occurs. The actual error code and error information are indicated by ErrorCode and ErrorInfo respectively in the response packet body.
For common error codes 60000 to 79999, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The private error codes for this API are as follows:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 90001 | Failed to parse the JSON format. Please check whether the request packet meets the JSON specifications, or whether the value of the To_Account field is an empty array. |
| 90003 | The value of the To_Account field in the JSON format request packet does not meet the message format requirements. Please check whether the type of the To_Account field is String. |
| 90009 | The administrator permissions of the app are required for the request. |
| 90011 | The number of target accounts for batch message delivery exceeds 500. Please decrease the value of the To_Account field. |
| 90992 | The backend service timed out. Please try again. |
| 90994 | Internal service error. Please try again. |
| 90995 | Internal service error. Please try again. |
| 91000 | Internal service error. Please try again. |

## API Debugging Tool
To debug this API, you can use the [Online REST API Debugging Tool](https://avc.qcloud.com/im/APITester/APITester.html#v4/openim/querystate).
