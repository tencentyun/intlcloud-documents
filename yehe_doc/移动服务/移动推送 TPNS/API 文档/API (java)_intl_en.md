## SDK Description
This SDK is used to encapsulate the TPNS server APIs and communicate with the TPNS server. To use it, you only need to import the `XingeApp` package. This SDK mainly encapsulates push-related V3 APIs.


## Integration Methods
Import Maven dependencies:

```
<dependency>
				<groupId>com.github.xingePush</groupId>
				<artifactId>xinge</artifactId>
				<version>1.2.4.2</version>
</dependency>
```

## Directions
### XingeApp API description
This class provides APIs for interaction with the TPNS server, which is constructed by `XingeApp.Builder` with the following parameters:

| Parameter Name | Type | Required | Default Value | Description |
| --- | --- | --- | --- | --- |
| appId | String | Yes | Empty | Push target `AccessID`, which can be obtained in the [Product Management](https://console.cloud.tencent.com/tpns) page in the console |
| secretKey | String | Yes | Empty | Push key |
| proxy | Proxy | No | Proxy.NO\_PROXY | This parameter can be set if a proxy needs to be configured |
| connectTimeOut | Integer | No | 10s | Connection timeout period |
| readTimeOut | Integer | No | 10s | Request timeout period |
| domainUrl | String | No | https://openapi.xg.qq.com/ | API request service domain name address, which is the XG API address by default. Change the value to the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to your service access point |

### Samples
``` java
XingeApp xingeApp = new XingeApp.Builder()
        .appId(appid)
        .secretKey(secretKey)
        .domainUrl("https://api.tpns.tencent.com/")    
        .build();

PushAppRequest pushAppRequest = new PushAppRequest();
// Complete the `PushAppRequest` message
... 
JSONObject ret =  xingeApp.pushApp(pushAppRequest );
```
### pushAppRequest API description
This class provides an encapsulated push message body. For the description and usage of parameters, please see [Push API Description](https://intl.cloud.tencent.com/document/product/1024/33764).

## Server Return Codes
For the meaning of `ret_code`, please see [Server-Side Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763).

## FAQs
1. What should I do if the error code 10101 or 403 is returned?
Check whether the application `AccessID` matches with `SecretKey`,  and whether `domainUrl` corresponds to the [service access point](https://intl.cloud.tencent.com/document/product/1024/38517) of the application.

2. What should I do if the error code 1008007 indicating parameter verification failure is returned?
Refer to [Push API](https://intl.cloud.tencent.com/document/product/1024/33764#ios-.E5.8D.95.E8.AE.BE.E5.A4.87.E6.8E.A8.E9.80.81.E8.AF.B7.E6.B1.82.E6.B6.88.E6.81.AF) and ensure that all the parameters are entered correctly.
