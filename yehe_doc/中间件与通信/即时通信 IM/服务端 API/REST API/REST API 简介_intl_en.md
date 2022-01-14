RESTful APIs are HTTP management APIs that provide the app backend with a management entry. For more information about RESTful APIs that IM supports, please see [RESTful API List](https://intl.cloud.tencent.com/document/product/1047/34621).
In addition to RESTful APIs, the app console also supports simple data management and one-to-one/group messaging. Developers can manage, check, and test data in the console. Even though RESTful APIs are less user-friendly, they provide powerful management capabilities.
For security concerns, RESTful APIs are supported over HTTPS only.

## Prerequisites
Before you call a RESTful API, complete the following operations:
1. Create an app in the IM console. For more information, see [Creating and Upgrading an Application](https://intl.cloud.tencent.com/document/product/1047/34577).
2. Assign an administrator account to the app. For more information, see the **Configuring Account Admins** section in [Basic Configuration](https://intl.cloud.tencent.com/document/product/1047/34540).

>!To avoid errors, please do use the administrator account when you call a RESTful API.

## Calling Method
### Request URL

The URL format of a RESTful API is as follows:
```
https://xxxxxx/$ver/$servicename/$command?sdkappid=$SDKAppID&identifier=$identifier&usersig=$usersig&random=99999999&contenttype=json
```


The descriptions and values ​​of parameters are as follows (parameter names and parameter values ​​are case-sensitive):

| Parameter  | Description  | Value  |
|---------|---------|---------|
| https    |Request protocol      | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  |   Exclusive domain name | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com` |
| ver  | Protocol version number | Always `v4`.  |
| servicename | Internal service name. Different values of `servicename` map to different service types. | Example:<br>For `v4/im_open_login_svc/account_import`, `im_open_login_svc` is the `servicename`.<br/>For more information, please see [RESTful API List](https://intl.cloud.tencent.com/document/product/1047/34621). |
| command | Command word. This is used with the `servicename` parameter to identify a specific service feature. | Example:<br>For `v4/im_open_login_svc/account_import`, `account_import` is the `command`.<br/>For more information, please see [RESTful API List](https://intl.cloud.tencent.com/document/product/1047/34621). |
| sdkappid | Application ID obtained in the IM console | It is obtained when a user applies for access. |
| identifier | Username, which must be the app administrator account when a RESTful API is called | For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Password that corresponds to the username | For more information, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random  | A parameter used to identify the current request | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype   |Request format     | Always `json`.                   |

>!
>- When the app server calls a RESTful API, `identifier` must be the app administrator account.
>- The app can generate a `UserSig` for the administrator account each time it calls a RESTful API, or generate a fixed `UserSig` for reuse with period of validity.

### HTTP request body format
RESTful APIs only support the POST method, and its request body is in JSON format. For more information about the request body format, please see the detailed description of each API.
Please note that POST request bodies cannot be empty. Even when no information is required in an HTTP request body, it still needs to carry an empty JSON object (`{}`).

### HTTP return code
The returned HTTP status code for RESTful APIs is always 200 unless a network error (such as error 502) occurs. The specific error code and error message are included in the HTTP response body.

### HTTP response body format
The RESTful API response body is in the JSON format and has the following elements:
```
{
    "ActionStatus": "OK", 
    "ErrorInfo": "", 
    "ErrorCode": 0
    // Other RESTful API response content
}
```
The response body must contain the `ActionStatus`, `ErrorInfo`, and `ErrorCode` fields. These three fields are described as follows:

| Field | Type| Description |
|---------|---------|---------|
|ActionStatus | String | Request result. OK: successful. FAIL: failed. If the request fails, the cause of failure is displayed in the `ErrorInfo` field. |
|ErrorInfo  | String | Failure causes |
| ErrorCode | Integer | Error code. 0: successful. Other values: failed. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348). |

## Sample Call
The following example shows how to use the [v4/group_open_http_svc/get_appid_group_list](https://intl.cloud.tencent.com/document/product/1047/34960) RESTful API to get all groups in an app.

HTTPS request:
```
POST /v4/group_open_http_svc/get_appid_group_list?usersig=xxx&identifier=admin&sdkappid=88888888&random=99999999&contenttype=json HTTP/1.1
Host: console.tim.qq.com
Content-Length: 22
{
    "Limit": 2
}
```
HTTPS response:
```
HTTP/1.1 200 OK
Server: nginx/1.7.10
Date: Fri, 09 Oct 2015 02:59:55 GMT
Content-Length: 156
Connection: keep-alive
Access-Control-Allow-Origin: *
Access-Control-Allow-Headers: X-Requested-With
Access-Control-Allow-Methods: POST

{
    "ActionStatus": "OK", 
    "ErrorCode": 0, 
    "GroupIdList": [
        {
            "GroupId": "@TGS#1YTTZEAEG"
        }, 
        {
            "GroupId": "@TGS#1KVTZEAEZ"
        }
    ], 
    "TotalCount": 58530
}
```

## RESTful API Common Error Codes

| Error Code |Description|
|---------|---------|
| 80001 | Text content filtering |
| 60002 | HTTP parsing error. Check the URL format of the HTTP request. |
| 60003 | JSON parsing error. Check the JSON format of the HTTP request. |
| 60004 | Account or signature error in the request URL or JSON request body. |
| 60005 | Account or signature error in the request URL or JSON request body. |
| 60006 | Invalid SDKAppID. Check the validity of SDKAppID. |
| 60007 | RESTful API call frequency limit exceeded. Reduce your request frequency. |
| 60008 | Service request timeout or HTTP request format error. Check and try again. |
| 60009 | Request resource error. Check the request URL. |
| 60010 | The request requires app administrator permissions. |
| 60011 | SDKAppID request frequency exceeded. Reduce your request frequency. |
| 60012 | SDKAppID is required for RESTful APIs. Check the SDKAppID parameter in the URL. |
| 60013 | JSON parsing error in the HTTP response body. |
| 60014 | Account switching timeout. |
| 60015 | Invalid account type in the request body. Make sure that the account is in string format. |

## FAQs
### The RESTful API request timed out and no response can be received.

1. The timeout period specified for the RESTful API in the IM backend is 3 seconds. You need to specify a timeout period that is longer than 3 seconds.
2. Run `telnet console.tim.qq.com 443` to check whether the service port is accessible.
3. Run `curl -I https://console.tim.qq.com` to test whether the status code is 200.
4. Check whether the machine uses a private or public DNS server. If the machine uses a private DNS server, make sure that the DNS server egress is in the same region of the ISP to which the egress IP of the machine belongs.
5. You are advised to use the "persistent connection+connection pool" mode.
