RESTful APIs are HTTP management APIs that provide the app backend with a management entry. For more information about RESTful APIs that IM supports, please see [RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/34621).
In addition to RESTful APIs, the app console also supports simple data management and one-to-one/group messaging. Developers can manage, check, and test data in the console. Even though RESTful APIs have fewer functions, they provide powerful management capabilities.
For security purposes, RESTful APIs are supported over HTTPS only.

## Prerequisites
To call a RESTful API, complete the following operations:
1. Create an app in the IM console. For more information, please see [Creating and Upgrading Applications](https://intl.cloud.tencent.com/document/product/1047/34577).
2. Assign an admin account to the app. For more information, please see account system integration in [Basic Configuration](https://intl.cloud.tencent.com/document/product/1047/34540).

> Use the app admin account to call RESTful APIs to prevent unnecessary call errors.

## Calling Method
### Request URL

The URL format of a RESTful API is as follows:
```
https://console.tim.qq.com/$ver/$servicename/$command?sdkappid=$SDKAppID&identifier=$identifier&usersig=$usersig&random=99999999&contenttype=json
```
The following table describes the parameters and their values (parameter names and values ​​are case-sensitive).

| Parameter | Description | Value |
|---------|---------|---------|
| https | Request protocol. | The request protocol is HTTPS, and the request method is POST. |
| console.tim.qq.com | Request domain name. | It has a fixed value of `console.tim.qq.com`. |
| ver | Protocol version. | It has a fixed value of `v4`. |
| servicename | Internal service name. Different servicename values map to different service types. | Example:<br>For `v4/im_open_login_svc/account_import`, `im_open_login_svc` is the `servicename`.<br/>For more information, please see [RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/34621). |
| command | Command word. This is used with the servicename parameter to identify a specific service feature. | Example:<br>For `v4/im_open_login_svc/account_import`, `account_import` is the `command`.<br/>For more information, please see [RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/34621). |
| sdkappid | App ID obtained in the IM console. | It is obtained when a user applies for access. |
| identifier | User name, which must be the app admin account when a RESTful API is called. | For more information, please see [App Admin](https://intl.cloud.tencent.com/document/product/1047/33517. |
| usersig | Password that corresponds to the user name. | For more information, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random number that identifies the current request. | It is a 32-bit unsigned random integer, ranging from 0 to 4294967295. |
| contenttype | Request format. | It has a fixed value of `json`. |

>
> 1. When the app server calls a RESTful API, the identifier must be the app admin account.
> 2. The app can generate a usersig for the admin account each time it calls a RESTful API or generate a fixed usersig for reuse within the usersig validity period.

### HTTP request body format
RESTful APIs only support the POST method, and its request body is in JSON format. For more information about the request body format, please see the detailed description of each API.
Note that POST request bodies cannot be empty. Even when no information is required in a protocol request body, it still needs to carry an empty JSON object, that is, `{}`.

### HTTP return code
Unless a network error (such as error 502) occurs, the HTTP return code for RESTful APIs is always 200. The HTTP response body returns the actual error code and error information.

### HTTP response body format
The RESTful API response body is in JSON format and has the following elements:
```
{
    "ActionStatus":"OK", 
    "ErrorInfo":"", 
    "ErrorCode": 0
    // Other RESTful API response content
}
```
The response body must contain the ActionStatus field, the ErrorInfo field, and the ErrorCode field. The following table describes these fields.

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | The request processing result. OK: succeeded. FAIL: failed. If the request fails, the ErrorInfo field displays the failure cause. |
| ErrorInfo | String | Failure cause. |
| ErrorCode | Integer | The error code. 0: succeeded. Other values: failed. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348). |

## Call Example
The following example shows how to use the [Obtaining All Groups in an App](https://intl.cloud.tencent.com/document/product/1047/34960) RESTful API to obtain all groups in an app.

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
Connection:keep-alive
Access-Control-Allow-Origin: *
Access-Control-Allow-Headers: X-Requested-With
Access-Control-Allow-Methods: POST

{
    "ActionStatus":"OK", 
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

| Error Code | Description |
|---------|---------|
| 80001 | Text security filtering |
| 60002 | HTTP parsing error. Check the URL format of the HTTP request. |
| 60003 | JSON parsing error. Check the JSON format of the HTTP request. |
| 60004 | The request URL or the account or signature in the JSON body is incorrect. |
| 60005 | The request URL or the account or signature in the JSON body is incorrect. |
| 60006 | Invalid SDKAppID. Check the SDKAppID validity. |
| 60007 | The RESTful API call frequency exceeded the limit. Reduce your request rate. |
| 60008 | The service request timed out, or the HTTP request format is incorrect. Check the error and try again later. |
| 60009 | Request resource error. Check the request URL. |
| 60010 | The request requires app admin permissions. |
| 60011 | The SDKAppID request frequency exceeded the limit. Reduce your request rate. |
| 60012 | SDKAppID is required for the RESTful API. Check the SDKAppID parameter in the URL. |
| 60013 | JSON parsing error in the HTTP response body. |
| 60014 | Account replacement timed out. |
| 60015 | Invalid account type in the request body. Confirm that the account is in string format. |

## FAQ
### The RESTful API request is timed out occasionally and no response can be received.

1. The timeout period specified for a RESTful API in the IM backend is 3 seconds. You need to specify a timeout period that is longer than 3 seconds.
2. Run telnet console.tim.qq.com 443 to check whether the service port is accessible.
3. Use curl -G https://console.tim.qq.com to test whether the response can be received.
4. Check whether the CVM uses a private or public DNS server. If the CVM uses a private DNS server, ensure that the DNS server egress IP address is in the same region of the ISP as the egress IP address of the CVM.
5. We recommend that the "persistent connection+connection pool" mode be used.
