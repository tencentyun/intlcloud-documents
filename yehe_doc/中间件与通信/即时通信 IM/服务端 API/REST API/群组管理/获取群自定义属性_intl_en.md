## Feature Description
 This API is used by the app admin to get custom group attributes.

## API Calling Description
### Applicable group types

| Group Type ID | RESTful API Support |
|-----------|------------|
| Private | No. Same as work groups (Work) in the new version. |
| Public | No |
| ChatRoom | No. Same as meeting group (Meeting) in the new version. |
| AVChatRoom | Yes |
|Community| No |


These are the preset group types in IM. For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

### Sample request URL
```
https://xxxxxx/v4/group_open_attr_http_svc/get_group_attr?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https | The request protocol is HTTPS, and the request method is POST. |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<li>China: `console.tim.qq.com`<li>Singapore: `adminapisgp.im.qcloud.com`<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com` |
| v4/group_open_attr_http_svc/get_group_attr | Request API                             |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype   |Request format, which should always be `json`.|

### Maximum call frequency

200 calls per second

### Sample request

- **Basic format**
Get custom attributes of a group.
```
{
    "GroupId": "@TGS#aC5SZEAEF"
}
```

### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | The ID of the group for which you want to get custom attributes |

### Sample response
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "GroupAttrAry": [
        {
            "key": "attr_key1",
            "value": "attr_val1"
        },
        {
            "key": "attr_key2",
            "value": "attr_val2"
        }
    ]
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode | Integer | Error code. `0`: successful; other values: failed |
| ErrorInfo | String | Error information |
| GroupAttrAry | Array | Key value pair for custom attributes |

## Error Codes
The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
|---------|---------|
| 10002 | Internal server error. Try again. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007 | No operation permissions. A group of this type does not support custom attributes. |
| 10010 | The group does not exist or has been deleted. |
| 10015 | Invalid group ID. Use a correct group ID. |
