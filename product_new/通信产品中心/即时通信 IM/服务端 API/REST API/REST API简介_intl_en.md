RESTful APIs are HTTP management APIs that provide the app backend with a management entry at the backend. For the list of RESTful APIs currently supported by IM, please see [RESTful APIs](https://cloud.tencent.com/document/product/269/1520).
The app console supports data management and one-to-one/group messaging. Developers can manage, check, and test data in the console. While RESTful APIs have less functions but they can provide more powerful management capabilities.
For security concerns, RESTful APIs are supported over HTTPS only.

## Prerequisites
Before you call the RESTful API, complete the following operations:
1. Create an app in the IM console. For more information, see [here](https://cloud.tencent.com/document/product/269/32577).
2. Assign an admin account to the app. For more information, see the account system in [Basic Configuration](https://cloud.tencent.com/document/product/269/32578).

>To avoid errors, please DO use the admin account when you call the RESTful API.

## Calling Method
### Request URL

The URL format of the RESTful API is as follows:
```
https://console.tim.qq.com/$ver/$servicename/$command?sdkappid=$SDKAppID&identifier=$identifier&usersig=$usersig&random=99999999&contenttype=json
```
The descriptions and values ​​of parameters are as follows (parameter names and parameter values ​​are case-sensitive):

| Parameter  | Description  | Value  |
|---------|---------|---------|
| https    |Request protocol.      | The request protocol is HTTPS, and the request method is POST.       |
| console.tim.qq.com |Request domain name.  | Always `console.tim.qq.com`.      |
| ver  | Protocol version number. | Always `v4`.  |
| servicename  | Internal service name. The servicename parameter varies with the service type. |Example:<br>`v4/im_open_login_svc/account_import`. `im_open_login_svc` is the `servicename`.<br/>For more information, see [RESTful APIs](https://cloud.tencent.com/document/product/269/1520). |
| command  | Command words. Used with the servicename parameter to identify a specific service feature. |Example:<br>`v4/im_open_login_svc/account_import`. `account_import` is the `command` parameter.<br/>For more information, see [RESTful APIs](https://cloud.tencent.com/document/product/269/1520). |
| sdkappid  | App ID obtained in the IM console. |It is obtained when the user applies for service connection. |
| identifier  | User name should be the admin account when the user calls the RESTful API. |For more information, see [App Admin](https://cloud.tencent.com/document/product/269/31999#app-.E7.AE.A1.E7.90.86.E5.91.98).  |
| usersig  | Password that corresponds to the user name. |For more information, see [Generating UserSig](https://cloud.tencent.com/document/product/269/32688). |
| random  | A random number parameter that is used to identify the current request. |32-bit unsigned random integer. Value range: 0-4294967295. |
| contenttype   |Request format.     | Always `json`.                   |

>
>1. When the app server calls the RESTful API, the identifier must be the app admin account.
>2. The app can generate a usersig for the admin account each time it calls the RESTful API, or generate a fixed usersig for reuse with period of validity.

### HTTP request body format
The RESTful API only supports the POST method, and its request body is in the JSON format. For more information about the request body format, see the detailed description of each API.
Please note that POST request bodies cannot be empty. Even when no information is required in the request body of an HTTP request, it still needs to carry an empty JSON object (`{}`).

### HTTP return code
The RESTful API typically returns a 200 OK status code unless a network error (such as the 502 Bad Gateway error) occurs. The specific error code and error message are included in the HTTP response body.

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
The response body must contain the ActionStatus field, the ErrorInfo field, and the ErrorCode field. These three fields are described as follows:

| Field | Type| Description |
|---------|---------|---------|
|ActionStatus | String | Result processing result. OK indicates success; FAIL indicates failure. If the request fails, the cause of failure is displayed in the ErrorInfo field. |
|ErrorInfo  | String | Failure causes |
|ErrorCode  | Integer | Error code. 0: Successful;  other values: Failed. For more information, see [Error codes](https://cloud.tencent.com/document/product/269/1671). |

## Example
This example shows you how to use the RESTful API to [obtain all groups in an app](https://cloud.tencent.com/document/product/269/1614).

HTTPS requests:
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

## RESTful API common error codes

| Error Code |Description|
|---------|---------|
| 80001 | Text security filtering |
| 60002 | HTTP parsing error. Please check the URL format of the HTTP request. |
| 60003 | JSON parsing error. Please check the JSON format of the HTTP request. |
| 60004 | Request URL or JSON body account or signature error. |
| 60005 | Request URL or JSON body account or signature error. |
| 60006 | Invalid SDKAppID. Please check the validity of SDKAppID. |
| 60007 | RESTful API request limit exceeded. Please reduce your request rate. |
| 60008 | Service request timed out or HTTP request format error. Check the error and try again later. |
| 60009 | Request resource error. Please check the request URL. |
| 60010 | The request requires app admin permission. |
| 60011 | SDKAppID request limit exceeded. Please reduce your request rate. |
| 60012 | SDKAppID is required for the RESTful API. Please check the SDKAppID parameter in the URL. |
| 60013 | JSON parsing error in the HTTP response body. |
| 60014 | Account replacement timed out. |
| 60015 | Invalid account type in the request body. Please confirm that the account is in string format. |

## FAQ
### The RESTful API request is timed out and no response can be received.

1. The timeout period specified for the RESTful API in the IM backend is 3 seconds. You need to specify a timeout period that is longer than 3 seconds.
2. Run telnet console.tim.qq.com 443 to check whether the service port is accessible.
3. Click https://console.tim.qq.com to test whether the response can be received.
4. Check whether the machine uses a private or public DNS server. If the machine uses a private DNS server, make sure that the DNS server egress is in the same region of the ISP to which the egress IP belongs.
5. We recommend using the "persistent connection+connection pool" mode.
