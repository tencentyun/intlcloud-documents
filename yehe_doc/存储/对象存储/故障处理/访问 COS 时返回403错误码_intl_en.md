## Symptoms

- 403 is returned when you use the APIs or SDKs of COS to upload/download files.
- 403 is returned when you access COS resources using a sub-account or temporary account.
- 403 is returned when you modify the bucket configuration.

## Troubleshooting

### Message: “Access Denied.”

If the following message is displayed when you access COS:
```
<Code>AccessDenied</Code>
<Message>Access Denied.</Message>
```

You can:

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** in the left sidebar.
3. Click the name of the desired bucket to go to the configuration page.
4. Click **Permission Management** > **Bucket ACL (Access Control List)**.
5. In the **Bucket ACL (Access Control List)** area, check whether the COS account is granted access permission.
 - If yes, proceed with the next step.
 - If not, click **Add User** and grant the account the permission needed.
![](https://main.qcloudimg.com/raw/795fe49c538f9e6a0fde44eee0a1c2af.png)
6. Verify whether the account has the granted permission.
 - If yes, proceed with the next step.
 - If not, click **Edit** to configure again.
7. In the **Permission Policy Settings** area, check whether a policy has been configured for the account.
>! 
>- If the bucket is set to **Private Read/Write** but anonymous access is set in the policy, the permission set in the policy takes effect.
>- If an action is set to **Allow** and **Deny** in different policies associated with the same sub-account, the action will be denied.
>- Policies set for **Everyone** have lower priorities than those set for a **Specified user**.
>
 - If yes, proceed with the next step.
 - If not, click **Add Policy** and add the needed permission to the sub-account that initiates the signed request.
![](https://main.qcloudimg.com/raw/a3bca9e3d7f0a2bea5d6f2387e2c5f90.png)
8. Verify whether the account has the granted permission.
 - If yes, proceed with the next step.
 - If not, click **Edit** to configure again.
9. Check whether the value of `q-ak` (case-sensitive) is the `secretID` and `secretKey` of the root account.
 - If yes, proceed with the next step.
 - If not, change the value of `q-ak` to the `secretID` and `secretKey` of the root account.
10. Check whether the resource is accessed by a cross-account.
 - If yes, authorize the sub-account by referring to [Authorizing Cross-Account’s Sub-account Read/Write Access to Specified File](https://cloud.tencent.com/document/product/598/11092).
 - If not, please [contact us](https://cloud.tencent.com/act/event/Online_service).


### Message: “AccessForbidden”

If the following message is displayed when you access COS:
```
<Code>AccessDenied</Code>
<Message>AccessForbidden</Message>
```

You can:

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** in the left sidebar.
3. Click the name of the desired bucket to go to the configuration page.
4. Click **Security Management** > **CORS (Cross-Origin Resource Sharing**.
5. In the **CORS (Cross-Origin Resource Sharing)** area, check whether it is a CORS request.
![](https://main.qcloudimg.com/raw/ddb551a419d8e622115906874061047d.png)
 - If yes, proceed with the next step.
 - If not, modify the CORS rule.
6. Run the following command to check whether the CORS request is correctly configured:
```
curl 'http://bucket-appid.cos.ap-guangzhou.myqcloud.com/object' -voa /dev/null -H 'Origin: origin set in the CORS configuration'
```
If the following message is displayed, the configuration is correct:
![](https://main.qcloudimg.com/raw/67513acee63f2f632b6cba58461fbe3d.png)

### Message: “You are denied by bucket referer rule”

If the following message is displayed when you access COS:
```
<Code>AccessDenied</Code>
<Message>You are denied by bucket referer rule</Message>
```

You can:

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** in the left sidebar.
3. Click the name of the desired bucket to go to the configuration page.
4. Click **Security Management** > **Hotlink Protection**.
5. In the **Hotlink Protection** area, check whether the configuration is correct (i.e. whether the request URL is added to the blocklist).
![](https://main.qcloudimg.com/raw/6190ed80abed7ddf4254325eb22019a6.png)
 - If yes, proceed with the next step.
 - If not, please [contact us](https://cloud.tencent.com/act/event/Online_service).
6. Run the following command to check whether hotlink protection is correctly configured:
```
curl 'http://bucket-appid.cos.ap-guangzhou.myqcloud.com/object' -voa /dev/null -H 'referer: the value of referer'
```
If the following message is displayed, the configuration is correct:
![](https://main.qcloudimg.com/raw/acc9862c6ffab6fd81c42136b775f2ea.png)


### Message: “InvalidAccessKeyId”

If the following message is displayed when you access COS:
```
<Code>AccessDenied</Code>
<Message>InvalidAccessKeyId</Message>
```

You can:

1. Check whether the `q-ak` value of `Authorization` in the request signature is correct.
 - If yes, proceed with the next step.
 - If not, modify the value of `q-ak` (case-sensitive), which should be the same as `SecretId` of the key.
2. Go to [Manage API Key](https://console.cloud.tencent.com/cam/capi) to check whether the API key is enabled.
![](https://main.qcloudimg.com/raw/9e69892ac2b9e8fe6b17f905b9599c7e.png)
 - If yes, please [contact us](https://cloud.tencent.com/act/event/Online_service).
 - If not, enable the API key.


### Message: “InvalidObjectState”

If the following message is displayed when you access COS:
```
<Code>AccessDenied</Code>
<Message>InvalidObjectState</Message>
```

You can:

Check whether the requested object is stored in ARCHIVE or DEEP ARCHIVE.
- If yes, restore the object first. For more information, please see [POST Object restore](https://cloud.tencent.com/document/product/436/12633).
- If not, please [contact us](https://cloud.tencent.com/act/event/Online_service).


### Message: “RequestTimeTooSkewed”

If the following message is displayed when you access COS:
```
<Code>AccessDenied</Code>
<Message>RequestTimeTooSkewed</Message>
```

You can:

1. Check the client-side time according to the OS as follows:
 - Windows (Windows Server 2012 is taken as an example): Click ![](https://main.qcloudimg.com/raw/ac22b052ee24273ebeab1139dd7f4d58.png) > **Control Panel** > **Clock, Language, and Region** > **Set the time and date**.
 - Linux: Run the `date -R` command.
![](https://main.qcloudimg.com/raw/88288162bd1de8c2ec0b640f0df6799e.png)
2. Check whether the clock skew between the client and server is larger than 15 minutes.
 - If yes, sync the clock.
 - If not, please [contact us](https://cloud.tencent.com/act/event/Online_service).


### Message: “Request has expired”

If the following message is displayed when you access COS:
```
<Code>AccessDenied</Code>
<Message>Request has expired</Message>
```

The possible causes are as follows:
- The signature has expired when you initiate the request.
- Your local system time is out of sync with the local time in your time zone.

You need to set the effective time of your signature again or sync the local system time. If the fault persists, please [contact us](https://cloud.tencent.com/act/event/Online_service).


### Message: “SignatureDoesNotMatch”

If the following message is displayed when you access COS:
```
<Code>AccessDenied</Code>
<Message>SignatureDoesNotMatch</Message>
```

You can:

Check whether the signature calculated on the client side is the same as that calculated on the server side.
- If yes, please [contact us](https://cloud.tencent.com/act/event/Online_service).
- If not, please see [Request Signature](https://cloud.tencent.com/document/product/436/7778).