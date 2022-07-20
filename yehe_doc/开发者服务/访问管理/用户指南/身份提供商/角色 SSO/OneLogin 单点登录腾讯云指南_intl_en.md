## Overview
OneLogin is a cloud identity access management solution provider. You can log in to all the internal system platforms of your organization through OneLogin's identity verification system with one click. Tencent Cloud supports identity federation with Security Assertion Markup Language 2.0 (SAML 2.0). SAML 2.0 is an open standard used by many IdPs such as OneLogin.
Federated single sign-on (SSO) can be implemented by using an IdP, and admins can authorize users with their federated identity authenticated to log in to the Tencent Cloud console or call TencentCloud APIs, eliminating the need to create a CAM sub-user for each employee in the organization.

This document describes how to configure OneLogin SSO to Tencent Cloud.

## Directions
### Creating a OneLogin enterprise application
>?
> - This step creates a OneLogin enterprise application. If you are already using one, skip this step and go straight to [CAM configuration](#cam).
> - This document uses the application name **test** as an example.
> 
1. Log in to the [OneLogin website](https://app.onelogin.com/login) and click **Applications** to enter the application management page.<span id="app"></span>
2. On the application management page, click **Add App** in the top-right corner.
3. In the search box, enter **SAML** and press **Enter**. In the results list, click **Pilot Catastrophe SAML (IdP)** as shown below:
![](https://main.qcloudimg.com/raw/2f80d98e0a6f05a589bd6a87323e56f7.png)
4. In **Display Name** field, enter the application name. Click **Save** in the top-right corner to complete the application creation as shown below:
![](https://main.qcloudimg.com/raw/a1bf87f51c2ff62838a1253e9e035bd1.png)

<span id="cam"></span>
### Configuring CAM
>? 
>- This step configures the trust relationship between OneLogin and Tencent Cloud.
> - In this example, the SAML IdP and role name are both **test**.
> 
1. On the [OneLogin application management page](#app), select the created application **test**.
2. Click **More Actions** in the top-right corner and select **SAML Matedata** to download the IdP cloud data file as shown below:
![](https://main.qcloudimg.com/raw/b109cd83a34d2f264a3697257d281715.png)
3. Create the Tencent Cloud CAM IdP and role. For detailed directions, see [Creating an IdP](https://intl.cloud.tencent.com/document/product/598/30391) and [Creating Role](https://intl.cloud.tencent.com/document/product/598/19381).

### Configuring OneLogin SSO
>?This step maps OneLogin application attributes to Tencent Cloud attributes to create the trust between the OneLogin application and Tencent Cloud.
>
1. On the [OneLogin application management page](#app), click the created **test** application to enter the application editing page.
2. Select the **Configuration** tab, enter the following content, and click **Save** as shown below:
![](https://main.qcloudimg.com/raw/2211da7f372415f536a81795d3a02207.png)

You can configure it based on the site of your Tencent Cloud account:
| Site | SAML Consumer URL| SAML Audience | SAML Recipient|
|---------|---------|---------|---------|
| Tencent Cloud International | https://intl.cloud.tencent.com/login/saml|https://intl.cloud.tencent.com/login/saml|https://intl.cloud.tencent.com/login/saml|

3. Click **Parameters**, select **Add Parameter**, and add the following two items:
<table>
	<tr>
		<th>Field name</th>
		<th>Flags</th>
		<th>Value</th>
		<th>Source Attribute</th>
	</tr>
	<tr>
		<td>https://cloud.tencent.com/SAML/Attributes/Role</td>
		<td>Include in SAML assertion</td>
		<td>Macro</td>	<td>qcs::cam::uin/{AccountID}:roleName/{RoleName1};qcs::cam::uin/{AccountID}:roleName/{RoleName2},qcs::cam::uin/{AccountID}:saml-provider/{ProviderName}</td>
	</tr>
		<tr>
		<td>https://cloud.tencent.com/SAML/Attributes/RoleSessionName</td>
		<td>Include in SAML assertion</td>
		<td>Macro</td>
		<td>Test</td>
	</tr>
</table>
>? Replace {AccountID}, {RoleName}, and {ProviderName} of the **Role** source attribute with the following content:
>- {AccountID}: Replace this with your Tencent Cloud account ID. You can view this in [Account Information in the console](https://console.cloud.tencent.com/developer).
>- {RoleName}: Replace this with the role name you created on Tencent Cloud. You can view this in [Role in the console](https://console.cloud.tencent.com/cam/role).
>- {ProviderName}: Replace this with the SAML IdP name that you created on Tencent Cloud. You can view this in [IdPs in the console](https://console.cloud.tencent.com/cam/idp).
>
4. Click **Save** in the top-right corner to save the configuration.

### Configuring a OneLogin user

1. Log in to the [OneLogin website](https://app.onelogin.com/login) and click **Users** to enter the user management page.
2. Click **New User** in the top-right corner to enter the user creation page.
3. <span id="step3"></span>Enter **First Name**, **Last Name**, **Email**, and **Username** and click **Save User** as shown below:
![](https://main.qcloudimg.com/raw/847476e48740284fb0754cf3e5d4e616.png)
>?Check your email for the password of this account, or click **More Actions** and select **Change Password** to change the password.
>
4. Click **Applications** on the user editing page. Select <image style="margin:0;" src="https://main.qcloudimg.com/raw/98a24d12696834b52f559d0abe490fd2.png"> on the right as shown below:
![](https://main.qcloudimg.com/raw/08ca65469c69a49b83c973ecfde2dc82.png)
5. In the pop-up window, select the SAML **test** application that you created. Click **Continue** as shown below:
![](https://main.qcloudimg.com/raw/5f653c7aea898a1648702ca35562fc6e.png)
6. On the editing page, click **Save** as shown below:
![](https://main.qcloudimg.com/raw/4e86052f6fc499ba368459bab532cc7a.png)
7. Use the account created in [step 3](#step3) to log in to OneLogin, and access the SAML **test** application created in the preceding sections. You will be redirected to the Tencent Cloud console.

