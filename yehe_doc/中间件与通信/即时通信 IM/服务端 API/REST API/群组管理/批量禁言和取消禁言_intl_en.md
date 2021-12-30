## Feature Description
- The app administrator can mute certain group members for a specific period of time.
- The app administrator can unmute certain group members.
- When muted users leave and then enter a group again, they remain muted.

## API Call Description
### Applicable group types

| Group Type ID | Support for This RESTful API |
|-----------|------------|
| Private | No. Same as work groups (Work) in the new version. |
| Public | Yes. |
| ChatRoom | Yes. Same as meeting groups (Meeting) in the new version. |
| AVChatRoom | Yes. |

Above are the IM built-in groups. For more information, please see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

>?Private groups (i.e., work groups in the new version）do not support muting members.

### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/forbid_send_msg?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Introduction](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/group_open_http_svc/forbid_send_msg | Request API |
| sdkappid | The SDKAppID assigned by the IM console when an application is created |
| identifier | The app administrator account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |


### Maximum call frequency

200 calls per second

### Sample request packets

- **Muting members**
You can set a specific period of time in `ShutUpTime` to mute specified members.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "Members_Account": [ // Up to 500 member accounts
        "peter",
        "leckie"
    ],
    "ShutUpTime": 60 // Muting period (unit: second)
}
```
- **Unmuting members**
To unmute members, set `ShutUpTime` to `0`.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "Members_Account": [ // Up to 500 member accounts
        "peter",
        "leckie"
    ],
    "ShutUpTime": 0 // 0 indicates to unmute members.
}
```

### Request packet fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | The ID of the group to be queried |
| Members_Account | Array | Yes | The member accounts to be muted. A maximum of 500 accounts are supported. |
| ShutUpTime | Integer | Yes | The muting period in seconds. `0` indicates to unmute members. `4294967295` indicates to permanently mute members. |

### Sample response packet

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode | Integer | Error code. `0`: successful. Other values: failed. |
| ErrorInfo | String | Detailed error information |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | Internal server error. Try again. |
| 10003 | Invalid command word. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007 | No operation permissions. For example, a common member in a public group tries to remove other users from the group, but only the app administrator can do so. |
| 10010 | The group does not exist or has been deleted. |
| 10015 | Invalid group ID. Make sure to use the correct group ID. |

## API Debugging Tool

Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/group_open_http_svc/forbid_send_msg) to debug this API.

## Reference
Getting the List of Muted Group Members ([v4/group_open_http_svc/get_group_shutted_uin](https://intl.cloud.tencent.com/document/product/1047/34964))
