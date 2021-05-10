## Prerequisites
Serverless Framework helps you quickly deploy your project to **Serverless SSR**. Before deploying, please make sure that you have [registered a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/10495).

## Authorization Method
### Authorizing by scanning code

When deploying by running `sls deploy`, you can scan the QR code for quick authorization and deployment. After you authorize by scanning the code, temporary key information will be generated (which will expire in 60 minutes) and written into the .env file in the current directory.
```
TENCENT_APP_ID=xxxxxx     # `AppId` of authorizing account
TENCENT_SECRET_ID=xxxxxx  # `SecretId` of authorizing account
TENCENT_SECRET_KEY=xxxxxx # `SecretKey` of authorizing account
TENCENT_TOKEN=xxxxx       # Temporary token
```
For more information on the permissions obtained during quick authorization, please see [SLS_QcsRole role permission list](#list).

>?If your account is a **Tencent Cloud sub-account**, policy authorization needs to be configured by the root account first. For more information on the configuration, please see [Configuring sub-account permission](#2).

### Authorizing with key

To eliminate the need for repeated authorization due to information expiration in case of authorization by scanning the code, you can authorize with a key. Create an `.env` file in the root directory of the project to be deployed and configure the Tencent Cloud `SecretId` and `SecretKey` information:

```
# .env
TENCENT_SECRET_ID=xxxxxxxxxx # `SecretId` of your account
TENCENT_SECRET_KEY=xxxxxxxx # `SecretKey` of your account
```

 You can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi). 

>?To ensure the account security, we recommend you use a **sub-account** key for authorization. The sub-account can deploy the project only after being granted the relevant permission. For more information on the configuration, please see [Configuring sub-account permission](#2).


<span id="2"></span>
## Sub-account Permission Configuration
### Configuration steps

If you use a Tencent Cloud sub-account, it does not have the operation permissions by default; therefore, it needs to be authorized by the **root account (or a sub-account with the authorization permission)** in the following steps:

1. On the [CAM User List](https://console.cloud.tencent.com/cam/user) page, select the target sub-account and click **Authorize**.
![](https://main.qcloudimg.com/raw/3d6e465aa4d6d50233e125e599475585.png)
2. Search for and select `QcloudSLSFullAccess` in the pop-up window and click **OK** to grant the sub-account the permission to manipulate all Serverless Framework resources.
![](https://main.qcloudimg.com/raw/80c98249cbdb327a80d8941ce54c962f.png)
3. On the [CAM User List](https://console.cloud.tencent.com/cam/user) page, select the target sub-account and click the username to enter the user details page.
![](https://main.qcloudimg.com/raw/00be606ee5a4f48dd956a8488f9f0d06.png)
4. Click **Associate Policy**. On the policy adding page, click **Select policies from the policy list** > **Create Custom Policy**.
Policy association page:
![](https://main.qcloudimg.com/raw/f08bcaaf91105a8fdb86a0487e6a734d.png)
Policy creation page:
![](https://main.qcloudimg.com/raw/47ac3d10b3dcae6d828ccc056393cee3.png)

5. Click **Create by Policy Syntax** > **Blank Template** and enter the following content. Be sure to replace the role parameter with your own `uin` (account ID):
```
   {
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cam:PassRole"
            ],
            "resource": [
                "qcs::cam::uin/${enter the account's uin}:roleName/SLS_QcsRole"
            ],
            "effect": "allow"
        },
        {
            "resource": [
                "*"
            ],
            "action": [
                "name/sts:AssumeRole"
            ],
            "effect": "allow"
        }
    ]
   }
```

6. After completing the custom policy configuration, go back to the authorization page in step 4, search for the custom policy just created, and click **Next** > **OK** to grant the sub-account the operation permissions of `SLS_QcsRole`. At this point, your sub-account should have a custom policy and a preset policy **QcloudSLSFullAccess** and can use Serverless Framework normally.
![](https://main.qcloudimg.com/raw/b062490a1703b7fac049c43c8e598c96.png)

>?In addition to the permission to call the default `SLS_QcsRole` role, you can also grant the sub-account the permission to call a custom role and control the sub-account permissions with refined permission policies in the custom role. For more information, please see [Configuring Role for Specified Operation](https://intl.cloud.tencent.com/document/product/1040/36819).

<span id="list"></span>
### SLS_QcsRole role permission list 

| Policy | Description |
| ----------------------- | ------------------------------------- |
| QcloudCOSFullAccess     | Full access to COS |
| QcloudSCFFullAccess     | Full access to SCF |
| QcloudSSLFullAccess     | Full access to SSL Certificate Service |
| QcloudTCBFullAccess     | Full access to TCB |
| QcloudAPIGWFullAccess   | Full access to API Gateway |
| QcloudVPCFullAccess     | Full access to VPC |
| QcloudMonitorFullAccess | Full access to Cloud Monitor |
| QcloudSLSFullAccess     | Full access to SLS (Serverless Framework) |
| QcloudCDNFullAccess     | Full access to CDN |
| QcloudCKafkaFullAccess  | Full access to CKafka |
| QcloudCodingFullAccess  | Full access to CODING DevOps    |
| QcloudPostgreSQLFullAccess | Full access to TencentDB for PostgreSQL |
| QcloudCynosDBFullAccess | Full access to TencentDB for CynosDB |
| QcloudCLSFullAccess    | Full access to CLS |
| QcloudAccessForSLSRole | This policy can be associated with the Serverless Framework (SLS) service role (SLS_QCSRole) for SLS' quick experience feature to access other Tencent Cloud service resources. It contains permissions of CAM-related operations. |
