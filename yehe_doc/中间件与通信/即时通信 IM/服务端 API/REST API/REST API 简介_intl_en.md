RESTful APIs are HTTP management APIs that provide the app backend with a management entry. For more information about RESTful APIs that Chat supports, see [RESTful API List](https://intl.cloud.tencent.com/document/product/1047/34621).
In addition to RESTful APIs, the app console also supports simple data management and one-to-one/group messaging. Developers can manage, check, and test data in the console. Even though RESTful APIs are less user-friendly, they provide powerful management capabilities.
For security concerns, RESTful APIs are supported over HTTPS only.

## Prerequisites
Before you call a RESTful API, complete the following operations:
1. Create an app in the Chat console. For more information, see [Creating and Upgrading an Application](https://intl.cloud.tencent.com/document/product/1047/34577).
2. Assign an admin account to the app. For more information, see the **Configuring Account Admins** section in [Basic Configuration](https://intl.cloud.tencent.com/document/product/1047/34540).

>!To avoid unnecessary call errors, use the admin account to call a RESTful API.

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
| xxxxxx | Dedicated domain name | <li>China: `console.tim.qq.com`</li><li>Singapore: `adminapisgp.im.qcloud.com`</li><li>Seoul: `adminapikr.im.qcloud.com`</li><li>Frankfurt: `adminapiger.im.qcloud.com`</li><li>Mumbai: `adminapiind.im.qcloud.com`</li><li>Silicon Valley: `adminapiusa.im.qcloud.com`</li> |
| ver  | Protocol version number | Always `v4`.  |
| servicename | Internal service name. Different values of `servicename` correspond to different service types. | Example:<br>For `v4/im_open_login_svc/account_import`, `im_open_login_svc` is the `servicename`.<br/>For more information, see [RESTful API List](https://intl.cloud.tencent.com/document/product/1047/34621). |
| command | Command word. This parameter is used with the `servicename` parameter to identify a specific service feature. | Example:<br>For `v4/im_open_login_svc/account_import`, `account_import` is the `command`.<br/>For more information, see [RESTful API List](https://intl.cloud.tencent.com/document/product/1047/34621). |
| sdkappid | App ID obtained in the Chat console | You can obtain the SDKAppID when applying for Chat SDK access. |
| identifier | Username, which must be the app admin account when a RESTful API is called | For more information, see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Password that corresponds to the user name. | For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random  | A parameter used to identify the current request | A random 32-bit unsigned integer ranging from 0 to 4,294,967,295 |
| contenttype   |Request format     | Always `json`.                   |

>!
>- When the app server calls a RESTful API, `identifier` must be the app admin account.
>- The app can generate a `UserSig` for the admin account each time it calls a RESTful API or generate a fixed `UserSig` for reuse with period of validity.

### HTTP request body format
RESTful APIs only support the POST method, and its request body is in JSON format. For more information about the request body format, see the detailed description of each API.
Note that POST request bodies cannot be empty. Even when no information is required in a request body, the request body still needs to carry an empty JSON object (`{}`).

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
|ActionStatus | String | Request result. `OK`: Successful. `FAIL`: Failed. If the request fails, the cause of failure is displayed in the `ErrorInfo` field. |
|ErrorInfo  | String | Failure causes |
| ErrorCode | Integer | Error code. `0`: Successful. Other values: Failed. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348). |

## Sample Call
The following example shows how to use the RESTful API to [get all groups in an app](https://intl.cloud.tencent.com/document/product/1047/34960).

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
| 60002 | HTTP parsing error. Check the URL format of the HTTP request. |
| 60003 | JSON parsing error. Check the JSON format of the HTTP request. |
| 60004 | Account or signature error in the request URL or JSON request body. |
| 60005 | Account or signature error in the request URL or JSON request body. |
| 60006 | Invalid SDKAppID. Check the validity of SDKAppID. |
| 60007 | RESTful API call frequency limit exceeded. Reduce your request frequency. |
| 60008 | Service request timeout or HTTP request format error. Check and try again. |
| 60009 | Request resource error. Check the request URL. |
| 60010 | The request requires app admin permissions. |
| 60011 | SDKAppID request frequency exceeded. Reduce your request frequency. |
| 60012 | SDKAppID is required for RESTful APIs. Check the SDKAppID parameter in the URL. |
| 60013 | JSON parsing error in the HTTP response body. |
| 60014 | Account switching timeout. |
| 60015 | Invalid account type in the request body. Make sure that the account is in string format. |
| 60016 | The SDKAppID is disabled. |
| 60017 | The request is disabled. |
| 60018 | Too many requests. Try again later. |
| 60019 | Too many requests. Try again later. |
| 60020 | Your Pro Edition has expired and was disabled. Log in to the [purchase page](https://buy.cloud.tencent.com/avc) and purchase it again. It will take effect in five minutes upon successful purchase. |
| 60021  | The source IP of the RESTful API call is invalid. |

## FAQs
### The RESTful API request timed out and no response was received.

1. The timeout period specified for the RESTful API in the Chat backend is three seconds. You need to specify a timeout period that is longer than three seconds.
2. Run `telnet console.tim.qq.com 443` to check whether the service port is accessible.
3. Run `curl -I https://console.tim.qq.com` to check whether the status code is 200.
4. Check whether the machine uses a private or public DNS server. If the machine uses a private DNS server, make sure that the DNS server egress is in the same region as the ISP to which the egress IP of the machine belongs.
5. You are advised to use the "persistent connection+connection pool" mode.
>?It is recommended that you use a RESTful API persistent connection to connect to the SDK. The reason is that it takes a long time to establish HTTPS non-persistent connections because each request causes TCP+TLS handshake overhead.
For scenario where a standard HTTP library is used: for HTTP 1.0, the request header `Connection: keep-alive` needs to be specified; for HTTP 1.1, persistent connections are supported by default; for scenarios where HTTPS requests are encapsulated based on TCP, TCP connections can be reused to send and receive requests.

