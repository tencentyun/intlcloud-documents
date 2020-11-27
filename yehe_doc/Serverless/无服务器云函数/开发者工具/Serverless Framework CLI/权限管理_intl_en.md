## Authorization Method
When deploying a project in Serverless Framework, you need to grant Serverless Framework permissions to manipulate your Tencent Cloud service resources through a [role](https://intl.cloud.tencent.com/document/product/598/19420) **by scanning the code** or **with a key**.

### Authorizing by scanning code
When you run the `sls` command, the system will query whether there is key information in the environment variables. If no key has been configured, a QR code will pop up for you to scan for authorization.

- After you scan the code with the root account, you can deploy the project through quick authorization. For more information on the permissions obtained during quick authorization, please see [SLS_QcsRole Role Permission List](#list).
- If you want to deploy by scanning the code with a sub-account, you need to configure policy authorization. For more information on the configuration, please see [Configuring sub-account permission](#2).

After you authorize by scanning the code, temporary key information will be generated (which will expire in 15 minutes) and written into the .env file in the current directory.

```
TENCENT_APP_ID=xxxxxx     # `AppId` of authorizing account
TENCENT_SECRET_ID=xxxxxx  # `SecretId` of authorizing account
TENCENT_SECRET_KEY=xxxxxx # `SecretKey` of authorizing account
TENCENT_TOKEN=xxxxx       # Temporary token
```

### Authorizing with key

To eliminate the need for repeated authorization due to information expiration in case of authorization by scanning the code, you can authorize with a key. Create an `.env` file in the root directory of the project to be deployed and configure the Tencent Cloud `SecretId` and `SecretKey` information:

```
# .env
TENCENT_SECRET_ID=xxxxxxxxxx # `SecretId` of your account
TENCENT_SECRET_KEY=xxxxxxxx # `SecretKey` of your account
```

 You can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi). 

To ensure the account security, we recommend you use a sub-account key for authorization. The sub-account can deploy the project only after being granted the relevant permission. For more information on the configuration, please see [Configuring sub-account permission](#2).



## Permission Configuration

 When deploying a project in Serverless Framework, you need to [use a role for authorization](https://intl.cloud.tencent.com/document/product/598/19420) as follows:
- The authorizing account should have the permission to manipulate the Serverless Framework service.
- The authorizing account should have the permission to call roles.
- The role to be called should have the policies that can manipulate the corresponding resources.

### Configuring root account permission
The root account has the permissions to manipulate the Serverless Framework service and call roles by default. The `SLS_QcsRole` role will be created by default when you [activate Serverless Framework](https://console.cloud.tencent.com/sls), which will have the corresponding policies of the associated services required by Serverless Framework during deployment. For the permissions of `SLS_QcsRole`, please see [SLS_QcsRole role permission list](#list).

<span id="2"></span>
### Configuring sub-account permission
A sub-account does not have the operation permissions by default; therefore, you need to authorize it with the **root account (or a sub-account with the authorization permission)** in the following steps:
1. [Grant the permission to manipulate the Serverless Framework service](#3).
2. [Grant the permission to call the `SLS_QcsRole` role](#4).

>?The `SLS_QcsRole` role has the corresponding policies of the associated services required by Serverless Framework during deployment. You can control the policies as instructed in [Configuring permission to manipulate specified role](#Configuring permission to manipulate specified role).

<span id="3"></span>
#### Granting permission to manipulate Serverless Framework service

When granting the sub-account permission to manipulate the Serverless Framework service, you can select the permission to manipulate all resources or specific resources.

##### Granting sub-account permission to manipulate all Serverless Framework resources

You can allow a sub-account to manipulate all Serverless Framework resources in the following steps:

1. On the [CAM User List](https://console.cloud.tencent.com/cam/user) page, select the target sub-account and click the username to enter the user details page.
2. Click **Associate Policy**. On the policy adding page, click **Select policies from the policy list**.
3. Search for and associate with `QcloudSLSFullAccess` and click **Next**.
4. Click **OK** to grant the sub-account the permission to manipulate all Serverless Framework resources.
   The policy syntax is as follows:

```json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "sls:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

##### Granting sub-account permission to manipulate specific Serverless Framework resources

You can allow a sub-account to manipulate only specific Serverless Framework resources in the following steps:

1. On the [CAM User List](https://console.cloud.tencent.com/cam/user) page, select the target sub-account and click the username to enter the user details page.
2. Click **Associate Policy**. On the policy adding page, click **Select policies from the policy list**.
3. Click **Create Custom Policy**, create a custom policy based on the policy syntax, and associate it with the user. The sample policy syntax is as shown below:

```json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "sls:*"
            ],
            "resource": "qcs::sls:ap-guangzhou::appname/${appname}/stagename/${stagename}",
            "effect": "allow"
        }
    ]
}
```

After the configuration is completed, the sub-account will have the permission to manipulate serverless applications only under `${appname}` and `${stagename}`.

<span id="4"></span>
#### Granting permission to call `SLS_QcsRole` role

A sub-account needs to be authorized by the root account to call the `SLS_QcsRole` role.

1. On the [CAM User List](https://console.cloud.tencent.com/cam/user) page, select the target sub-account and click the username to enter the user details page.
2. Click **Associate Policy**. On the policy adding page, click **Select policies from the policy list**.
3. Click **Create Custom Policy** > **Create by Policy Syntax** > **Blank Template** and enter the following content. Be sure to replace the role parameter with your own `uin` (account ID):
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
4. Click **OK** to grant the sub-account the permission to manipulate `SLS_QcsRole`.

#### Configuring permission to manipulate specified role 

 In addition to the permission to call the `SLS_QcsRole` role, you can also grant the sub-account the permission to call a custom role and control the sub-account permissions with refined permission policies in the custom role. For more information, please see [Configuring Role for Specified Operation](https://intl.cloud.tencent.com/document/product/1040/36819).

<span id="list"></span>
## SLS_QcsRole Role Permission List 

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
| QcloudAccessForSLSRole | This policy can be associated with the Serverless Framework (SLS) service role (SLS_QCSRole) for SLS' quick experience feature to access other Tencent Cloud service resources. It contains permissions of CAM-related operations. |

>!The full access to SLS (Serverless Framework) is a new permission added to the new version of Serverless Framework. If you use the key on a legacy version for deployment and want to switch to the new version, you need to delete the key and log in again.



