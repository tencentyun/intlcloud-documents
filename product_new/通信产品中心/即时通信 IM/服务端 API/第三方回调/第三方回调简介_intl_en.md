## Overview

To implement refined control over app features, IM provides you with powerful callbacks for free. These callbacks use the persistent connection mode by default. A callback refers to that the IM backend sends a request to the app backend server before or after an event occurs. This allows the app backend to synchronize data as required or intervene in the subsequent event processing. For more information on the callbacks currently supported by IM, see the [Callback Command List](https://intl.cloud.tencent.com/document/product/1047/34355).

A third-party callback is sent to the app backend server through an HTTP or HTTPS request, and the app backend server must process the IM callback request and respond as soon as possible. By taking the [callback before delivering a group message](https://intl.cloud.tencent.com/document/product/1047/34374) as an example, before the message is sent, the IM backend sends a callback request to the app backend server and determines whether to deliver the message based on the callback result. Through the callback, the app can synchronize the message or perform security filtering on the delivered message. The following figure shows the callback process.
![](https://main.qcloudimg.com/raw/c4aca82a8601caf27bf14f5765592e28.svg)

## Callback Classification

Callbacks can be classified into four types according to their features:
- Online status callback
- Profile relationship chain callback
- One-to-one chat message callback
- Group system callback

Callbacks can be divided into two types from the processing perspective:
- Callback before an event occurs: this callback is designed to allow the app backend to intervene in the processing logic of the event. IM determines the subsequent processing flow based on the return code of the callback. For example, the callback before sending group messages belongs to this type of callbacks.
- Callback after an event occurs: this callback is designed to allow the app backend to perform required data synchronization. In this case, IM ignores the return code of the callback. For example, the callback after a member quits belongs to this type of callbacks.

## Callback Protocol

Third-party callbacks are based on the HTTP or HTTPS protocol. The app backend must provide a callback URL to IM, and IM initiates a callback request to the app backend through a POST request. When initiating the callback request, IM appends the following parameters to the end of the URL provided by the app backend:

| Parameter | Description |
|---------|---------|
| SdkAppid | The app ID assigned by IM. |
| CallbackCommand | The callback command keyword. |
| contenttype | This parameter is optional and its value is JSON in most cases. |
| ClientIP | The client IP address. |
| OptPlatform | The client platform. Depending on the platform type, one of the following values applies: <br />RESTAPI (requests are sent through RESTful APIs), Web (requests are sent through web SDKs), and <br/>Android, iOS, Windows, Mac, and Unknown (requests are sent through an unknown device.) |

The specific content of the callback is included in the HTTP request packet. For details, see the callback example below.

## Callback Example

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

## Callback Timeout Period

The timeout period for an IM callback to the app backend is 2 seconds, after which the callback is not retried. If the callback times out, the subsequent processing logic is the same as that with the callback not configured. For example, if the callback before sending group messages times out, the message will be delivered normally.

To ensure a high callback success rate, third-party apps need to process callbacks quickly. For example, the app can return the callback response and then process the specific business logic.

## Security Considerations

IM supports three types of callbacks:

1. HTTP callback.
2. HTTPS callback. The WebServer of the app backend is configured with a certificate issued by a CA or a certificate issued by IM for free.
3. HTTPS mutual authentication callback. The WebServer of the app backend is configured with a certificate issued by a CA or a certificate issued by IM for free, and mutual authentication is enabled.

The first type of callbacks have the lowest security level, and the last type of callbacks have the highest security level.

1. HTTP callbacks have two defects. One is that data transmitted in plain text is prone to interception, and the other is that the third-party app cannot determine whether the callback request comes from IM.
2. For an HTTPS callback, if mutual authentication is disabled, the data encryption issue can be resolved, but the app still cannot determine whether the callback request comes from IM.
3. Only the combination of HTTPS callbacks and mutual authentication can ensure the security of third-party callbacks.

We strongly recommend that apps use the third type of callbacks. In addition, the certificate issued by IM is completely free of charge.

## Callback Configuration

Currently, the IM console allows you to configure callbacks, including configuring callback URLs and allowed callbacks. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).

> The IM console allows you to configure only HTTP and HTTPS callbacks. To enable the HTTPS mutual authentication callback, which has the highest security level, complete the following steps:
> 1. In the IM console, configure the callback URL (which must be an HTTPS domain name) and enable callback.
> 2. Submit a ticket to IM. IM will then issue the certificate required for mutual authentication to the app. In this case, the following information must be specified in the ticket:
> 1. SDKAppID
> 1. App name
> 1. Callback URL, which must be consistent with that set in the console
> 3. After receiving the certificate, configure HTTPS mutual authentication by referring to these guidelines:
> 1. [Configuring HTTPS mutual authentication on an Apache server](https://intl.cloud.tencent.com/document/product/1047/34379)
> 1. [Configuring HTTPS mutual authentication on a Nginx server](https://intl.cloud.tencent.com/document/product/1047/34380)

## Common Reasons for Callback Failures

If a callback fails, check whether the configured callback service is normal according to the following checklist:

| Callback Failure Symptom | Possible Reason |
| --- | --- |
| Accessing the callback URL times out | 1. IM cannot complete DNS resolution. In this case, check whether the domain name is valid on the public network. For example, if the URL of the callback host is `http://notexist.com`, IM cannot complete DNS resolution because the domain name does not exist. <br>2. IM cannot access the IP address set in the callback URL. In this case, check whether this IP address is accessible from the public network. For example, if the URL of the callback host is `http://10.0.0.1`, IM cannot access the IP address because it is a private IP address of the app. <br>3. The failure occurs due to the firewall policy of the app callback service. In this case, check the firewall configuration. For example, an invocation failure occurs if the app callback server is configured to deny all requests through port 80. |
| Access is denied by the callback service | IM can access the host but fails to establish a connection. In this case, check whether WebServer has started properly. For example, a callback failure occurs when the WebServer of the app callback server has not started or when the port configuration is incorrect. |
| HTTPS certificate configuration of the callback service is incorrect | This problem can occur when the callback type is HTTPS (or HTTPS mutual authentication), in which case IM can access the app callback server, but determines that the certificate configured on the app WebServer is invalid. In this case, check that the HTTPS certificate is correctly configured. |
| HTTPS mutual authentication configuration of the callback service is incorrect | This problem can occur when the callback type is HTTPS mutual authentication. In this case, IM verifies that the certificate configured on the app callback server is valid, but the app callback server fails to verify the IM certificate. |
| HTTP return code of the callback service is not 200 | The callback request succeeded, but the HTTP return code in the response packet is not 200. |
| Callback response packet cannot be parsed | The callback response packet is not in JSON format. |
