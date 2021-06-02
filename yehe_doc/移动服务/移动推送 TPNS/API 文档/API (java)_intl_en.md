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

| Parameter             | Type    | Required                          | Default Value                   | Description                                                         |
| -------------- | ------- | ---- | -------------------------- | ------------------------------------------------------------ |
| appId | String | Yes | Empty | Push target `AccessID`, which can be obtained on the [Product Management](https://console.cloud.tencent.com/tpns) page in the console. |
| secretKey      | String  | Yes   | Empty                         | Push key, which can be obtained on the [**Product Management**](https://console.cloud.tencent.com/tpns) > **Configuration Management** > **Basic Configuration** page.                                                     |
| proxy          | Proxy   | No   | Proxy.NO\_PROXY            | This parameter can be set if a proxy needs to be configured.|
| connectTimeOut | Integer | No   | 10s                        | Connection timeout period.                                             |
| readTimeOut    | Integer | No   | 10s                        | Request timeout period.                                             |
| domainUrl | String | No | https://openapi.xg.qq.com/ | API request service domain name address, which is the XG API address by default. Change the value to the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to your service access point. |

#### Sample

```java
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

This class provides an encapsulated push message body. For the description and usage of parameters, please see [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).
## Samples
>? The `XingeAppSimple` class provides API examples related to message push, account binding and unbinding, etc.

### Push to a single Android device

```java
public JSONObject pushTokenAndroid() {
        PushAppRequest pushAppRequest = new PushAppRequest();
        pushAppRequest.setAudience_type(AudienceType.token);
        pushAppRequest.setMessage_type(MessageType.notify);
        Message message = new Message();
        message.setTitle("title");
        message.setContent("content");
        pushAppRequest.setMessage(message);
        MessageAndroid messageAndroid = new MessageAndroid();
        message.setAndroid(messageAndroid);
        ArrayList<String> tokenList = new ArrayList();
        tokenList.add("04cac74a714f61bf089********63d880993");
        pushAppRequest.setToken_list(tokenList);
        return this.xingeApp.pushApp(pushAppRequest);
    }
```

### Push to a single Android account

```java
public JSONObject pushAccountAndroid() {
        PushAppRequest pushAppRequest = new PushAppRequest();
        pushAppRequest.setAudience_type(AudienceType.account);
        pushAppRequest.setPlatform(Platform.android);
        pushAppRequest.setMessage_type(MessageType.notify);
        pushAppRequest.setAccount_push_type(1);
        Message message = new Message();
        message.setTitle("title");
        message.setContent("content");
        MessageAndroid messageAndroid = new MessageAndroid();
        message.setAndroid(messageAndroid);
        pushAppRequest.setMessage(message);
        ArrayList<String> accountList = new ArrayList();
        accountList.add("123");
        pushAppRequest.setAccount_list(accountList);
        return this.xingeApp.pushApp(pushAppRequest);
    }
```

### Push to Android devices with specified tags

```java
public JSONObject pushTagAndroid() {
        PushAppRequest pushAppRequest = new PushAppRequest();
        pushAppRequest.setAudience_type(AudienceType.tag);
        pushAppRequest.setPlatform(Platform.android);
        pushAppRequest.setMessage_type(MessageType.notify);
        Message message = new Message();
        message.setTitle("title");
        message.setContent("content");
        MessageAndroid messageAndroid = new MessageAndroid();
        message.setAndroid(messageAndroid);
        pushAppRequest.setMessage(message);
        ArrayList<String> tagList = new ArrayList();
        tagList.add("tag");
        TagListObject tagListObject = new TagListObject();
        tagListObject.setTags(tagList);
        tagListObject.setOp(OpType.OR);
        pushAppRequest.setTag_list(tagListObject);
        return this.xingeApp.pushApp(pushAppRequest);
    }
```

### Push to all Android devices

```java
public JSONObject pushAllAndroid() {
        PushAppRequest pushAppRequest = new PushAppRequest();
        pushAppRequest.setAudience_type(AudienceType.all);
        pushAppRequest.setPlatform(Platform.android);
        pushAppRequest.setMessage_type(MessageType.notify);
        Message message = new Message();
        message.setTitle("title");
        message.setContent("content");
        MessageAndroid messageAndroid = new MessageAndroid();
        message.setAndroid(messageAndroid);
        pushAppRequest.setMessage(message);
        return this.xingeApp.pushApp(pushAppRequest);
    }
```
### Push to a single iOS device

```java
public JSONObject pushTokenIos(){
        PushAppRequest pushAppRequest = new PushAppRequest();
        pushAppRequest.setAudience_type(AudienceType.token);
        pushAppRequest.setEnvironment(Environment.valueOf("dev"));
        pushAppRequest.setMessage_type(MessageType.notify);
        Message message = new Message();
        message.setTitle("title");
        message.setContent("content");
        MessageIOS messageIOS = new MessageIOS();
        Alert alert = new Alert();
        Aps aps = new Aps();
        aps.setAlert(alert);
        messageIOS.setAps(aps);
        message.setIos(messageIOS);
        pushAppRequest.setMessage(message);
        ArrayList<String> tokenList = new ArrayList<String>();
        tokenList.add("0250df875c93c55********536b54fc1c49f");
        pushAppRequest.setToken_list(tokenList);
        return this.xingeApp.pushApp(pushAppRequest);
    }
    
```

### Push to a single iOS account

```java
 public JSONObject pushAccountIos() {
        PushAppRequest pushAppRequest = new PushAppRequest();
        pushAppRequest.setAudience_type(AudienceType.account);
        pushAppRequest.setEnvironment(Environment.valueOf("dev"));
        pushAppRequest.setMessage_type(MessageType.notify);
        Message message = new Message();
        message.setTitle("Account push");
        message.setContent("content");
        MessageIOS messageIOS = new MessageIOS();
        Alert alert = new Alert();
        Aps aps = new Aps();
        aps.setAlert(alert);
        messageIOS.setAps(aps);
        message.setIos(messageIOS);
        pushAppRequest.setMessage(message);
        ArrayList<String> accountList = new ArrayList();
        accountList.add("1122");
        pushAppRequest.setAccount_list(accountList);
        return this.xingeApp.pushApp(pushAppRequest);
    }
    
```

### Push to iOS devices with specified tags

```java
public JSONObject pushTagIos() {
        PushAppRequest pushAppRequest = new PushAppRequest();
        pushAppRequest.setAudience_type(AudienceType.tag);
        pushAppRequest.setEnvironment(Environment.valueOf("dev"));
        pushAppRequest.setMessage_type(MessageType.notify);
        Message message = new Message();
        message.setTitle("Tag push");
        message.setContent("content");
        MessageIOS messageIOS = new MessageIOS();
        Alert alert = new Alert();
        Aps aps = new Aps();
        aps.setAlert(alert);
        messageIOS.setAps(aps);
        message.setIos(messageIOS);
        pushAppRequest.setMessage(message);
        ArrayList<String> tagList = new ArrayList();
        tagList.add("1122");
        TagListObject tagListObject = new TagListObject();
        tagListObject.setTags(tagList);
        tagListObject.setOp(OpType.OR);
        pushAppRequest.setMessage(message);
        pushAppRequest.setTag_list(tagListObject);
        return this.xingeApp.pushApp(pushAppRequest);
    }
    
```

### Push to all iOS devices

```java
public JSONObject pushAllIos() {
        PushAppRequest pushAppRequest = new PushAppRequest();
        pushAppRequest.setAudience_type(AudienceType.all);
        pushAppRequest.setEnvironment(Environment.valueOf("dev"));
        pushAppRequest.setMessage_type(MessageType.notify);
        Message message = new Message();
        message.setTitle("Full push");
        message.setContent("content");
        MessageIOS messageIOS = new MessageIOS();
        Alert alert = new Alert();
        Aps aps = new Aps();
        aps.setAlert(alert);
        messageIOS.setAps(aps);
        message.setIos(messageIOS);
        pushAppRequest.setMessage(message);
        return this.xingeApp.pushApp(pushAppRequest);
    }

    
```

### Push response sample

```java
{"result":"{}","environment":"","push_id":"1328245138690125824","err_msg":"NO_ERROR","err_msg_zh":"","ret_code":0,"seq":0}
```

## Server Return Codes

For the meaning of `ret_code`, please see [Server-Side Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763).

## FAQs

#### What should I do if the error code 10101 or 403 is returned?
Check whether the application `AccessID` matches with `SecretKey`, and whether `domainUrl` corresponds to the [service access point](https://intl.cloud.tencent.com/document/product/1024/38517) of the application.

#### What should I do if the API returns the error code 1008007 that indicates invalid parameters?
Refer to [Push API](https://intl.cloud.tencent.com/document/product/1024/33764#ios-.E5.8D.95.E8.AE.BE.E5.A4.87.E6.8E.A8.E9.80.81.E8.AF.B7.E6.B1.82.E6.B6.88.E6.81.AF) and enter all the parameters correctly.
