## Overview
This document describes how to **configure a permission policy in the TEM console** and use CAM to **grant the policy to a sub-account**.

## Directions
1. Log in to the [TEM console](https://console.cloud.tencent.com/tem/policy?rid=1) and click **Permission management** on the left sidebar.
2. On the **Permission management** page, click **Create permission policy** and enter a policy name and description.
![](https://qcloudimg.tencent-cloud.cn/raw/3a86b5734ef912d86d60012fbc09d516.png)
3. (Optional) Authorize environment resources:
![](https://qcloudimg.tencent-cloud.cn/raw/b1457ca050a19a2a46f6c19053a5744a.png)
 - Select **Environment** and select the operation and resource scopes in the options expanded below.
 - Select the scope of environment operations to be authorized:
     - **View environment details**: This option includes read operations and deployment operations (deploying applications and associate gateways to the environment) of the selected environment.
     - **Manage environment**: This option includes the read, deployment, and write operations of the selected environment.
 - Select the scope of environment resources to be authorized:
 	  - **Specified environments**: You can select resources in the resource selector below.
	- **All environments**: This option refers to all existing environments and includes those added subsequently.
4. (Optional) Authorize application resources:
![](https://qcloudimg.tencent-cloud.cn/raw/fb8091812be010b4daff24b88bb875dd.png)
 - Select **Application** and select the operation and resource scopes in the options expanded below.
 - Select the scope of application operations to be authorized:
 	  - **View application details**: This option includes read operations of the selected application.
 	  - **Manage application**: This option includes the read and write operations of the selected application.
 - Select the scope of application resources to be authorized:
 	  - **Specified applications**: You can select resources in the resource selector below.
 	  - **All applications**: This option refers to all existing applications and includes those added subsequently.
5. (Optional) Authorize CLB gateway resources:
![](https://qcloudimg.tencent-cloud.cn/raw/5c57c6304ce2969181f52c5f0aa95f66.png)
 - Select **CLB gateway** and select the operation and resource scopes in the options expanded below.
 - Select the scope of CLB gateway operations to be authorized:
 	  - **View CLB gateway details**: This option includes the read operations of the selected CLB gateway.
 	  - **Manage CLB gateway**: This option includes the read and write operations of the selected CLB gateway.
 - Select the scope of CLB gateway resources to be authorized:
 	  - **Specified CLB gateway**: You can select resources in the resource selector below.
     - **All CLB gateways**: This option refers to all existing CLB gateways and includes those added subsequently.
6. Preview the configured permission policy content, confirm that everything is correct, and click **Confirm and go to CAM for authorization**. You will be redirected to the **CAM Policy Generation** page.
![](https://qcloudimg.tencent-cloud.cn/raw/12ea90e4deb1f41eccdcb93b3cd735b5.png)
7. **Generate the corresponding permission policy** in CAM and click **Complete**.
>! Do not modify the generated policy content; otherwise, the policy may not take effect.
8. **Associate the generated policy to the target users/user groups** to complete authorization.
