Currently, Serverless Framework can deploy a project properly only with the relevant [role](https://intl.cloud.tencent.com/document/product/598/19420) permissions in the `SLS_QcsRole` role under the account. This role contains the policies for products that are used in deployment with Serverless Framework. You can configure the permissions for a root account or sub-account.

## Root Account Permission Configuration
Currently, you can grant permissions by configuring the account key. As the root account has the permissions to create roles and bind policies, you can associate it with `SLS_QcsRole` for Serverless Framework access in the following way: 

### Authorization through account key configuration

If you want to configure persistent environment variables/key information so that you do not need to deploy them by scanning the code every time, you can create a `.env` file under the project directory and save the `SecretId` and `SecretKey` information.
```ini
# .env
TENCENT_SECRET_ID=123  // Your `SecretId` 
TENCENT_SECRET_KEY=123 // Your `SecretKey`
```
Serverless Framework will check whether the user is in Mainland China by default during deployment. If your development environment is outside Mainland China and you want to use Serverless Framework in the Mainland China edition, you can add the following configuration in the `.env` file to start the Mainland China edition by default, which provides an interactive quick deployment process (for more information, please see [Getting Started](https://intl.cloud.tencent.com/document/product/1040/36249)).
```ini
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
SERVERLESS_PLATFORM_VENDOR=tencent
```

>?
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).

## Sub-account Permission Configuration

If you want to grant a sub-account the permission to deploy by scanning code, you need to ensure that the sub-account has permissions to create roles and bind role policies. You can add the preset policy `QcloudCamRoleFullAccess` or `QcloudCamSubaccountsAuthorizeRoleFullAccess` to the sub-account.

You can also add `SLS_QcsRole` by using the root account in the [CAM Console](https://console.cloud.tencent.com/cam/role) to grant access to Serverless Framework resources. The role entity is `sls.cloud.tencent.com`, which includes the following policy permissions:
- QcloudCDNFullAccess
- QcloudTCBFullAccess
- QcloudSLSFullAccess
- QcloudSSLFullAccess
- QcloudCKafkaFullAccess
- QcloudMonitorFullAccess
- QcloudVPCFullAccess
- QcloudCOSFullAccess
- QcloudAPIGWFullAccess
- QcloudSCFFullAccess

After the creation is successful, the root account needs to bind the following two policies to the sub-account:
1. [Call permission policy of a specified role](#1)
2. [API permission policy of Serverless Framework](#2)

<span id="1"></span>
### Granting sub-account permission to call specified role
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
                "qcs::cam::uin/000000000000:roleName/SLS_QcsRole"
            ],
            "effect": "allow"
        }
    ]
}
```
4. Click **OK** to grant the sub-account the permission to manipulate SLS_QcsRole.

<span id="2"></span>
### Granting sub-account permission to use APIs of Serverless Framework

Two authorization methods are provided below for your reference:

#### Method 1. Grant the sub-account permission to manipulate all Serverless Framework resources
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

#### Method 2. Grant the sub-account permission to manipulate specific Serverless Framework resources

You can allow a sub-account to manipulate only specific Serverless Framework resources in the following steps:
1. On the [CAM User List](https://console.cloud.tencent.com/cam/user) page, select the target sub-account and click the username to enter the user details page.
2. Click **Associate Policy**. On the policy adding page, click **Select policies from the policy list**.
3. Click **Create Custom Policy**, create a custom policy based on the policy syntax, and associate it to the user. The sample policy syntax is as shown below:
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
