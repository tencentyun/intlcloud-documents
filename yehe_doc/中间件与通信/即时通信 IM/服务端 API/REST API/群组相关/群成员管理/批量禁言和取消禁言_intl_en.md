## Feature Overview
- The app administrator can mute certain group members for a specific period of time.
- The app administrator can unmute certain group members.
- When muted users leave and then enter the group again, they remain muted.

## API Calling Description
### Applicable group types

| Group Type | Support for This RESTful API |
|-----------|------------|
| Private | No. Same as work groups (Work) in the new version. |
| Public | Yes |
| ChatRoom | Yes. Same as meeting groups (Meeting) in the new version. |
| AVChatRoom | Yes |
| Community | Yes |

Above are the built-in group types of the Chat service. For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

>?Private groups (i.e., work groups in the new version) do not support muting members.

### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/forbid_send_msg?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters

The following table describes the modified parameters when this API is called. For other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<br><li>China: `console.tim.qq.com`</li><li>Singapore: `adminapisgp.im.qcloud.com`</li><li>Seoul: `adminapikr.im.qcloud.com`</li><li>Frankfurt: `adminapiger.im.qcloud.com`</li><li>Mumbai: `adminapiind.im.qcloud.com`</li><li>Silicon Valley: `adminapiusa.im.qcloud.com`</li> |
| v4/group_open_http_svc/forbid_send_msg | Request API |
| sdkappid | SDKAppID assigned by the Chat console when an app is created |
| identifier | App admin account. For more information, see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295. |
| contenttype | Request format. The value is fixed to `json`. |

### Maximum call frequency

200 calls per second

### Sample request

- **Muting members**
You can set a specific period of time in `MuteTime` to mute specified members.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "Members_Account": [ // Up to 500 member accounts
        "peter",
        "leckie"
    ],
    "MuteTime": 60 // Muting period, in seconds
}
```
- **Unmuting members**
To unmute members, set `MuteTime` to `0`.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "Members_Account": [ // Up to 500 member accounts
        "peter",
        "leckie"
    ],
    "MuteTime": 0 // 0 indicates to unmute members.
}
```

### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | The ID of the group to be queried |
| Members_Account | Array | Yes | The member accounts to be muted. A maximum of 500 accounts are supported. |
| MuteTime| Integer | Yes | Muting period of the unsigned integer type, in seconds. `0`: Unmute; `4294967295`: Permanent muting  |
|TopicId|String| Optional | ID of the topic whose muting status is to be set. This field applies only to topic-enabled community groups. |

### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode":0
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode | Integer | Error code. `0`: Successful; other values: Failed |
| ErrorInfo | String | Error information |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | Internal server error. Try again. |
| 10003 | Invalid command word. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007 | No operation permissions. For example, a common member in a public group tries to remove other users from the group, but only the app admin can do so. |
| 10010 | The group does not exist or has been deleted. |
| 10015 | Invalid group ID. Use the correct group ID. |

## API Debugging Tool

Use the [RESTful API online debugging tool](https://tcc.tencentcs.com/im-api-tool/index.html#/v4/group_open_http_svc/forbid_send_msg) to debug this API.

## References
Getting the List of Muted Group Members ([v4/group_open_http_svc/get_group_muted_account](https://intl.cloud.tencent.com/document/product/1047/34964))

