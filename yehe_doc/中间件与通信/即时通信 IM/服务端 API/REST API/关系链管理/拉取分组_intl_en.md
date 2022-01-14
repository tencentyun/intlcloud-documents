## Feature Description 

This API is used to pull friend lists. You can specify the lists to pull and pull the friends in the lists.



## API Calling Description

### Sample request URL

```

https://xxxxxx/v4/sns/group_get?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json

```


### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).


| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com` |
| v4/sns/group_get | Request API |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |



### Maximum calling frequency



200 calls per second



### Sample request packets

- **Basic request**
```

{
  "From_Account":"id", 
  "LastSequence":1
}


```


- **Complete request**
```

{

     "From_Account":"id", 

     "NeedFriend":"Need_Friend_Type_Yes", 

     "LastSequence":1, 

     "GroupName":["group1"]

}



```



### Request packet fields

| Field | Type | Required | Description |
|----|-----|------|-----|
| From_Account | String | Yes | `UserID` of the account for which to pull friend lists |
| LastSequence | Integer | Yes | Sequence of the last list pull returned by the backend to the client. The value is `0` for the first pull. This field is valid only when `GroupName` is left empty. |
| NeedFriend | String | No | Whether to pull the users in the list. `Need_Friend_Type_Yes`: pulls users. If this field is left empty, users will not be pulled. It is valid only when `GroupName` is left empty. |
| GroupName | Array | No | Name of the list to pull |

### Sample response packets

- **Response to a basic request**
```

{

    "ResultItem": [

        {

            "GroupName": "group1",

            "FriendNumber": 1

        },

        {

            "GroupName": "group2",

            "FriendNumber": 2

        },

        {

            "GroupName": "group3",

            "FriendNumber": 3

        }

    ],

    "CurrentSequence": 2,

    "ActionStatus": "OK",

    "ErrorCode": 0,

    "ErrorInfo": "",

    "ErrorDisplay": ""

}

```

- **Response to a complete request**
```

{

    "ResultItem": [

        {

            "GroupName": "group1",

            "FriendNumber": 1,

            "To_Account": ["friend1"]

        }  

    ],

    "CurrentSequence": 2,

    "ActionStatus": "OK",

    "ErrorCode": 0,

    "ErrorInfo": "",

    "ErrorDisplay": ""

}

```



### Response packet fields

| Field | Type | Description |
|-----|-------|------|
|ResultItem | Array  | Result object array of pulling lists|
|GroupName| String  | List name |
| FriendNumber | Integer | Number of friends in the list |
| To_Account | Array | `UserID` of friends in the list |
| CurrentSequence | Integer  | Current sequence of the lists  |
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode | Integer | Error code. `0`: successful; other values: failed. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ErrorInfo | String | Detailed error information |
| ErrorDisplay | String | Detailed information displayed on the client |

[](id:ErrorCode)

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ResultCode`, `ResultInfo`, `ErrorCode`, and `ErrorInfo`.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30001 | Incorrect request parameter. Check your request according to the error description. |
| 30003 | The requested account does not exist. |
| 30004 | The request requires app admin permissions. |
| 30006 | Internal server error. Try again. |
| 30007 | Network timeout. Try again later. |



## API Debugging Tool

Use the [RESTful API online debugging tool](https://tcc.tencentcs.com/im-api-tool/index.html#v4/sns/group_get) to debug this API.



## References

- Adding Lists (<a href="https://intl.cloud.tencent.com/document/product/1047/34950">v4/sns/group_add</a>)
- Deleting Lists (<a href="https://intl.cloud.tencent.com/document/product/1047/34926">v4/sns/group_delete</a>)
