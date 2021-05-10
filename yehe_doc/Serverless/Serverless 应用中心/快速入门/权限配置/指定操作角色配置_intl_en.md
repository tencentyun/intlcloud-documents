In addition to the default role `SLS_QcsRole`, a root account can also create multiple custom roles and assign them to sub-users, so that they can have only the policies granted by the corresponding roles as needed, which can implement permission control. Its flowchart is as follows:
![](https://main.qcloudimg.com/raw/90591c64f093fa2e016aeb1c1ae55c0c.png)

## Root Account Configuration Process
You can create a sub-account, configure a role, and grant the role the corresponding policies. The following uses the deployment of an SCF function triggered by API Gateway as an example:

### Creating sub-account role
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/role) with your root account and click **Role** on the left sidebar.
2. On the role page, click **Create Role** and select **Tencent Cloud Service** as the role entity.
3. Among the services supporting roles, select **Serverless Framework (sls)** and click **Next**.
4. Select presets policies **QcloudCOSFullAccess**, **QcloudAPIGWFullAccess**, and **QcloudSCFFullAccess** and click **Next**.	
5. Enter a role name such as `test-role1` and click **Complete**.
You can click the role name to view the role page after configuration:
![](https://main.qcloudimg.com/raw/6313089678ae0a5d229a2c7426e9a586.png)


### Configuring role policy
1. Click **[Policy](https://console.cloud.tencent.com/cam/policy)** on the left sidebar to enter the policy management page.
2. On the policy management page, click **Create Custom Policy** and select **Create by Policy Syntax**.
3. Select **Blank Template** as the policy template and click **Next**.
4. Enter the policy name and content and click **Complete**.
Bind the role policy. Here, you need to populate the `resource` parameter with the six-segment description of the role to be bound to the sub-account:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cam:PassRole"
            ],
            "resource": [
                # Six-segment role description (such as `qcs::cam::uin/123456789:roleName/test-role1`)
            ],
            "effect": "allow"
        }
    ]
}
```
>?The role resource description can be obtained on the role information page.


### Associating sub-user with policy
1. Click **User** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar to enter the user list page.
2. Select the sub-user to be authorized and click **Authorize** in the "Operation" column.
3. Select the created policy and the preset policy **QcloudSLSFullAccess** in the policy list and click **OK** to associate them with the target sub-account so as to bind the role.
4. **(Optional)** If you think that `QcloudSLSFullAccess` contains excessive permissions, you can create a custom policy to grant a specified resource the SLS call permission with the following policy template:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "sls:*"
            ],
            "resource": [
                # Enter the project resource name (such as `qcs::sls:ap-guangzhou::appname/*`)
            ],
            "effect": "allow"
        }
    ]
}
```
>?The project resource description must strictly follow the CAM specifications. You can also describe the resource more specifically by entering a function name or stage name.

## Sub-account Configuration Process
  Create a Serverless project locally, add a global configuration item `configRole` in the `serverless.yaml` configuration file, and enter the role name. After the backend successfully checks the permissions, the deployment will be completed.
```
# serverless.yml

component: scf # Name of the imported component, which is required. The `tencent-scf` component is used in this example
name: scfdemo # Name of the instance created by this component, which is required
org: test # Organization information, which is optional. The default value is the `appid` of your Tencent Cloud account
app: scfApp # SCF application name, which is optional
stage: dev # Information for identifying environment, which is optional. The default value is `dev`

globalOptions:
   configRole: test-role1     # Name of specified role, which is optional

inputs:
  name: scfFunctionName
  src: ./src
  runtime: Nodejs10.15 # Runtime environment of function. Valid values: Python2.7, Python3.6, Nodejs6.10, Nodejs8.9, Nodejs10.15, PHP5, PHP7, Go1, Java8.
  region: ap-guangzhou
  handler: index.main_handler
  events:
    - apigw:
        name: serverless_api
        parameters:
          protocols:
            - http
            - https
          serviceName:
          description: The service of Serverless Framework
          environment: release
          endpoints:
            - path: /index
              method: GET

```   
>!
>- If no role is bounded, the sub-account will use `SLS_QcsRole` for SLS deployment by default, and the `configRole` parameter does not need to be set in the configuration file.
>- Once a role is bounded, please check the `configRole` name in the `yaml` file carefully. An error will be reported if the value is incorrect or empty. A sub-account can use only bounded roles but cannot use other roles.

## Granting Permission to Sub-account
If you want to grant a permission to a sub-account, you need to provide the role name and the name of the policy to be associated together to the root account. Then, the root account can grant the permission in [CAM Console](https://console.cloud.tencent.com/cam/role) > **Role**.
