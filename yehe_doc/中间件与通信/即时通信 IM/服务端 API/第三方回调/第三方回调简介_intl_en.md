## Overview

To give you refined control over app features, IM provides you with powerful callbacks free of charge. The callbacks use persistent connection mode by default. A callback means that the IM backend sends a request to the app backend server before or after an event occurs. This allows the app backend to synchronize data if necessary or intervene in the subsequent event processing. For more information about the callbacks currently supported by IM, see the [Callback Command List](https://intl.cloud.tencent.com/document/product/1047/34355).

A third-party callback is sent to the app backend server using an HTTP/HTTPS request, and the app backend server must process the IM callback request and provide a response as soon as possible. Take the [callback before delivering a group message](https://intl.cloud.tencent.com/document/product/1047/34374) as an example. Before the message is sent, the IM backend sends a callback request to the app backend server and determines whether the message should be sent based on the callback result. Based on the callback, the app can synchronize the message. The following figure shows the callback process.
![](https://main.qcloudimg.com/raw/617414146c22be3c874e3af3b3e2234c.png)

## Callback Classification

Callbacks can be classified into four types according to their functions:
- Online status callbacks
- Profile and relationship chain callbacks
- One-to-one message callbacks
- Group system callbacks

Callbacks can be classified into two types by process:
- Callback before an event occurs: the purpose of this type of callback is to allow the app backend to intervene in the processing logic of the event. IM will determine the subsequent processing flow based on the return code of the callback. For example, the callback before a group message is sent is this type of callback.
- Callback after an event occurs: the purpose of this type of callback is to allow the app backend to implement essential data synchronization. IM ignores the return codes of such callbacks. For example, the callback after a member quits a group is this type of callback.

## Callback Protocol

Third-party callbacks are based on HTTP/HTTPS protocols. The app backend must provide a callback URL to IM, and IM uses a POST request to initiate a callback request to the app backend. When initiating a callback request, IM adds the following parameters at the end of the URL provided by the app backend:

| Parameter | Description |
|---------|---------|
| SdkAppid | App ID assigned by IM |
| CallbackCommand | Callback command word |
| contenttype | Optional. The value is generally a JSON string. |
| ClientIP | IP address of the client |
| OptPlatform | Client platform. Depending on the platform type, the following values are available: <br />RESTAPI (requests are sent using RESTful APIs) and Web (requests are sent using Web SDKs), <br/>Android, iOS, Windows, Mac, iPad, and Unknown (requests are sent using an unknown device). |
>?"IOS" (all in uppercase) is used in the `State.StateChange` callback, while "iOS" (the first letter is in lowercase) is used in other callbacks. Please perform compatibility processing during use.

The specific callback content is included in the HTTP request packet. For details, see the following callback examples.

## Callback Examples

Callback request example:

```
POST /?SdkAppid=888888&CallbackCommand=Group.CallbackAfterNewMemberJoin&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform HTTP/1.1
Host: www.example.com
Content-Length: 337
{
    "CallbackCommand": "Group.CallbackAfterNewMemberJoin", 
    "GroupId": "@TGS#2J4SZEAEL", 
    "Type": "Public", 
    "JoinType": "Apply", 
    "Operator_Account": "leckie", 
    "NewMemberList": [
        {
            "Member_Account": "jared"
        }, 
        {
            "Member_Account": "tommy"
        }
    ]
}
```

Callback response example:

```
HTTP/1.1 200 OK
Server: nginx/1.7.10
Date: Fri, 09 Oct 2015 02:59:55 GMT
Content-Length: 75
{
    "ActionStatus": "OK", 
    "ErrorInfo": "", 
    "ErrorCode": 0
}
```

## Callback Timeout Period and Retry

The timeout period for IM callbacks to the app backend is 2 seconds.

Before event occurrence, callbacks are not retried. After event occurrence, callbacks are not retried by default, and you can configure whether to retry the callbacks when they time out.

To ensure a high callback success rate, third-party apps need to process callbacks quickly. For example, the app can send a callback response and then process the specific business logic.

## Handling Policy for Callback Timeouts Before Event Occurrence

If a callback times out before event occurrence, the default policy is to deliver the message.

You can configure the handling policy for callback timeouts before event occurrence in the console. For example, when a callback timeout occurs before a group message is sent, you can specify whether to deliver the message. 

## Security Considerations

IM supports three types of callbacks:

1. HTTP callback
2. HTTPS callback. The WebServer of the app backend is configured with a certificate issued by a CA or a certificate issued by IM free of charge.
3. HTTPS mutual authentication callback. The WebServer of the app backend is configured with a certificate issued by a CA or a certificate issued by IM free of charge, and mutual authentication is enabled.

>?To get a certificate issued by IM free of charge, you need to log in to the console and configure callback URL and download the certificate. For more information, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).

The first type of callback has the lowest security level, and the last type has the highest security level.

1. HTTP callbacks have two defects. One is that data transmitted in plain text is vulnerable to interception, and the second is that a third-party app cannot determine whether the callback request really comes from IM.
2. For an HTTPS callback, if mutual authentication is disabled, the data encryption issue can be resolved, but the app still cannot ensure that the callback request comes from IM.
3. Only the combination of HTTPS callback and mutual authentication can ensure the security of third-party callbacks.

We strongly recommend that apps use the third type of callback. In addition, the certificate issued by IM is completely free of charge.

## Callback Configuration

Currently, the IM console allows you to configure callbacks, including configuring the callback URL and the types of callback enabled. For details on the configuration methods, see [Configuration of Third-Party Callbacks](https://intl.cloud.tencent.com/document/product/1047/34520).

>!The IM console allows you to configure only HTTP and HTTPS callbacks. If you need to enable the HTTPS mutual authentication callback, which has the highest security level, perform the following steps:
> 1. On the IM console, configure the callback URL (which must be an HTTPS domain name) and enable the callback.
>2. Click **Download HTTPS Mutual Authentication Certificate** on the right to get the certificate. Configure HTTPS mutual authentication according to the following:
>   1. [Configuring HTTPS Mutual Authentication on an Apache Server](https://intl.cloud.tencent.com/document/product/1047/34379)
>   2. [Configuring HTTPS Mutual Authentication on an Nginx Server](https://intl.cloud.tencent.com/document/product/1047/34380)

## Common Reasons for Callback Failures

If a callback failure occurs, check whether the configured callback service has a problem according to the following checklist:

| Callback Failure Symptom | Possible Reason |
| --- | --- |
| Access to the callback URL times out | 1. IM cannot complete DNS resolution. In this case, check whether the domain name is valid on the public network. For example, if the callback host is `http://notexist.com`, IM cannot complete DNS resolution because this domain name does not exist. <br>2. IM cannot access the IP address configured in the callback URL. In this case, check whether this IP address is accessible from the public network. For example, if the callback host is `http://10.0.0.1`, IM cannot access this IP address because the domain name is a private IP address of the app.<br>3. The failure occurs due to the firewall policy of the app callback service. In this case, check the firewall configuration. For example, a callback failure occurs if the app callback server denies all requests arriving at port 80. |
| Access denied by the callback service | IM can access the host, but a connection is not established. In this case, check whether the WebServer has started properly. For example, a callback failure will occur when the WebServer of the app callback server has not started or when the port configuration is incorrect. |
| HTTPS certificate configuration error of the callback service | This can occur when the callback type is HTTPS (or HTTPS mutual authentication). IM can access the app callback server, but determines that the certificate configured on the app WebServer is invalid. In this case, check that the HTTPS certificate is properly configured. |
| HTTPS mutual authentication configuration error of the callback service | This can occur when the callback type is HTTPS mutual authentication. IM verifies that the certificate configured on the app callback server is valid, but the app callback server fails to verify the IM certificate. |
| The HTTP return code of the callback service is not 200 | The callback request is successful, but the HTTP return code in the response packet is not 200. |
| The callback response packet could not be parsed | The callback response packet is not in JSON format. |
