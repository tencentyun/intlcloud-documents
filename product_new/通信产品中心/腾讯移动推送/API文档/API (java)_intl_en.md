## SDK Description
This SDK provides the Java package of the TPNS server APIs and communicates with the TPNS backend. You can import the `XingeApp` package when using it. This SDK mainly encapsulates v3 APIs related to push.
## Integration Steps
Import Maven dependencies:
Resource library configuration:
``` xml
 <repositories>
        <repository>
            <id>xingePush</id>
           <url>https://raw.githubusercontent.com/xingePush/maven-repository/snapshot/</url>
     </repository>
    </repositories>
```

Dependency configuration
```
<dependency>
            <groupId>com.github.xingePush</groupId>
            <artifactId>xinge</artifactId>
            <version>1.2.2</version>
</dependency>
```

## Directions
### XingeApp API description
This class provides APIs for interaction with the TPNS backend and constructed by `XingeApp.Builder` with the following parameters:

| Parameter Name | Type | Required | Default Value | Description |
| --- | --- | --- | --- | --- |
| appId | int | Yes | None | Push target `accessID` (which is a 10-digit number starting with 1500 for Android or 1600 for iOS) |
| secretKey | String | Yes | None | Push key |
| proxy | Proxy | No | Proxy.NO\_PROXY | This parameter can be set if a proxy needs to be configured |
| connectTimeOut | int | No | 10s | Connection timeout period |
| readTimeOut | int | No | 10s | Request timeout period |
| domainUrl | String | No | https://openapi.xg.qq.com/ | API request service domain name address, which is the TPNS API address by default and should be changed to `https://api.tpns.tencent.com/` during use |

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
## Server Return Code
For the meaning of `ret_code`, please see [Server Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763).
