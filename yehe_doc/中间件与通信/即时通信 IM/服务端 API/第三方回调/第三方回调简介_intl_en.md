## Overview

To give you refined control over app features, Chat provides you with powerful webhooks free of charge. The webhooks use persistent connection mode by default. A webhook means that the Chat backend sends a request to the app backend server before or after an event occurs. This allows the app backend to synchronize data if necessary or intervene in the subsequent event processing. For more information about the webhooks currently supported by Chat, see the [Webhook Command List](https://intl.cloud.tencent.com/document/product/1047/34355).

A webhook is sent to the app backend server using an HTTP/HTTPS request, and the app backend server must process the Chat webhook request and provide a response as soon as possible. Take the [Before Group Message Is Sent](https://intl.cloud.tencent.com/document/product/1047/34374) webhook event as an example. Before the message is sent, the Chat backend sends a webhook request to the app backend server and determines whether the message should be sent based on the webhook result. Based on the webhook, the app can synchronize the message. The following figure shows the webhook process.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/PnuW853_1.png)

## Webhook Classification

Webhooks can be classified into four types according to their functions:
- Online status webhooks
- Relationship chain webhooks
- One-to-one message webhooks
- Group webhooks

Webhooks can be classified into two types by process:
- Webhook before an action occurs: the purpose of this type of webhook is to allow the app backend to intervene in the processing logic of the event. Chat will determine the subsequent processing flow based on the return code of the webhook. For example, the webhook before a group message is sent is this type of webhook.
- Webhook after an action occurs: the purpose of this type of webhook is to allow the app backend to implement essential data synchronization. Chat ignores the return codes of such webhooks. For example, the webhook after a member quits a group is this type of webhook.

## Webhook Protocol

Webhooks are based on HTTP/HTTPS protocols. The app backend must provide a webhook URL to Chat, and Chat uses a POST request to initiate a webhook request to the app backend. When initiating a webhook request, Chat adds the following parameters at the end of the URL provided by the app backend:

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| SdkAppid        | App ID assigned by Chat                                      |
| CallbackCommand | Webhook command word                                         |
| contenttype     | Optional. The value is generally a JSON string.              |
| ClientIP        | IP address of the client                                     |
| OptPlatform     | Client platform. Depending on the platform type, the following values are available: <br />`RESTAPI` (requests are sent using RESTful APIs) and `Web` (requests are sent using Web SDKs), <br/>`Android`, `iOS`, `Windows`, `macOS`, `iPad`, and `Unknown` (requests are sent using an unknown device). |
>?"IOS" (all in uppercase) is used in the `State.StateChange` webhook, while "iOS" (the first letter is in lowercase) is used in other webhooks. Please perform compatibility processing during use.

The specific webhook content is included in the HTTP request packet. For details, see the following webhook examples.

## Webhook Examples

Webhook request example:

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

Webhook response example:

```
HTTP/1.1 200 OK
Server: nginx/1.7.10
Date: Fri, 09 Oct 2015 02:59:55 GMT
Content-Length: 75
{
    "ActionStatus": "OK", 
    "ErrorInfo": "", 
    "ErrorCode":0
}
```

## Webhook Timeout Period and Retry

The timeout period for Chat webhooks to the app backend is two seconds.

Before event occurrence, webhooks are not retried. After event occurrence, webhooks are not retried by default, and you can configure whether to retry the webhooks when they time out.

To ensure a high webhook success rate, third-party apps need to process webhooks quickly. For example, the app can send a webhook response and then process the specific business logic.

## Handling Policy for Webhook Timeouts Before Event Occurrence

If a webhook times out before event occurrence, the default policy is to deliver the message.

You can also configure the handling policy for webhook timeouts before event occurrence in the console. For example, when a webhook timeout occurs before a group message is sent, you can specify whether to deliver the message.

## Security Considerations

Chat supports both HTTP and HTTPS webhooks. For HTTPS webhooks, you need to configure a certificate issued by a CA or a certificate issued by Chat free of charge in the WebServer of the app backend.

>?To get a certificate issued by Chat free of charge, you need to log in to the console and configure webhook URL and download the certificate. For more information, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).

Related security issues are as follows:

1. HTTP transmits data in plain text, and data confidentiality cannot be guaranteed. Therefore, HTTPS is recommended.
2. It's impossible to determine whether a webhook request really comes from Chat.

For request source security, we provide two solutions:
1. Webhook authentication (recommended)
<dx-alert infotype="explain" title="Configuration guide">
1. Configure the webhook URL and enable webhook in the console.
2. During webhook URL configuration, enable authentication and configure the authentication token. Then, the signature (`Sign`) and signing timestamp (`RequestTime`) will be added to the webhook request URL. The signature algorithm is **Sign=sha256(TokenRequestTime)**.
3. The app backend authenticates the webhook request. It uses SHA256 to calculate and verify the signature based on the local authentication token and the signing timestamp (`RequestTime`) in the webhook URL.
</dx-alert>
```
Signature algorithm sample:

Token=xxxyyy
RequestTime=1669872112
Sign=sha256(xxxyyy1669872112)=17773bc39a671d7b9aa835458704d2a6db81360a5940292b587d6d760d484061

Webhook URL=URL&Sign=17773bc39a671d7b9aa835458704d2a6db81360a5940292b587d6d760d484061&RequestTime=1669872112
```
2. HTTPS mutual authentication
<dx-alert infotype="explain" title="Configuration guide">
1. On the Chat console, configure the webhook URL (which must be an HTTPS domain name) and enable webhook.
2. Click **Download HTTPS Mutual Authentication Certificate** on the right to get the certificate. Configure HTTPS mutual authentication according to the following:
   1. [Configuring HTTPS Mutual Authentication on an Apache Server](https://intl.cloud.tencent.com/document/product/1047/34379)
   2. [Configuring HTTPS Mutual Authentication on an Nginx Server](https://intl.cloud.tencent.com/document/product/1047/34380)
   </dx-alert>

## Common Reasons for Webhook Failures

If a webhook failure occurs, check whether the configured webhook service has a problem according to the following checklist:

| Webhook Failure Symptom                                      | Possible Reason                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Access to the webhook URL times out                          | 1. Chat cannot complete DNS resolution. In this case, check whether the domain name is valid on the public network. For example, if the webhook host is `http://notexist.com`, Chat cannot complete DNS resolution because this domain name does not exist. <br>2. Chat cannot access the IP address configured in the webhook URL. In this case, check whether this IP address is accessible from the public network. For example, if the webhook host is `http://10.0.0.1`, Chat cannot access this IP address because the domain name is a private IP address of the app.<br>3. The failure occurs due to the firewall policy of the app webhook service. In this case, check the firewall configuration. For example, a webhook failure occurs if the app webhook server denies all requests arriving at port 80. |
| Access denied by the webhook service                         | Chat can access the host, but a connection is not established. In this case, check whether the WebServer has started properly. For example, a webhook failure will occur when the WebServer of the app webhook server has not started or when the port configuration is incorrect. |
| HTTPS certificate configuration error of the webhook service | This can occur when the webhook type is HTTPS (or HTTPS mutual authentication). Chat can access the app webhook server, but determines that the certificate configured on the app WebServer is invalid. In this case, check that the HTTPS certificate is properly configured. |
| HTTPS mutual authentication configuration error of the webhook service | This can occur when the webhook type is HTTPS mutual authentication. Chat verifies that the certificate configured on the app webhook server is valid, but the app webhook server fails to verify the Chat certificate. |
| The HTTP return code of the webhook service is not 200       | The webhook request is successful, but the HTTP return code in the response packet is not 200. |
| The webhook response packet could not be parsed              | The webhook response packet is not in JSON format.           |
