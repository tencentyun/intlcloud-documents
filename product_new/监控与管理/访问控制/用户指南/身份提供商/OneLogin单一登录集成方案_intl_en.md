## Introduction
OneLogin is a cloud identity access management solution provider. You can log in to all the internal system platforms of an enterprise through OneLogin’s identity verification system with one click. Tencent Cloud supports identity federation with SAML 2.0 (Security Assertion Markup Language 2.0). SAML 2.0 is an open standard used by many identity providers (IdPs) such as OneLogin. Federated single sign-on can be implemented by using an identity provider, and admins can authorize users that have their federated identity authenticated to log in to the Tencent Cloud console or to call Tencent Cloud APIs, without requiring the creation of a CAM sub-user for each employee of the enterprise or organization.
This tutorial describes how to configure OneLogin single sign-on for Tencent Cloud.

## Directions
### Creating OneLogin Enterprise Applications
>
> - This step creates a OneLogin enterprise application. If you’re already using one, please skip this step and go straight to [CAM configuration](#cam).
> - This document uses the application name **test** as an example.

1. Log in and access the [OneLogin Application Management page](https://xiaoyu.onelogin.com/apps). Click **Add App**.
2. In the search box, enter **SAML** and press **Enter**. In the results list, click **Pilot Catastrophe SAML (IdP)**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/2f80d98e0a6f05a589bd6a87323e56f7.png)
3. In **Display Name** field, enter the application name and click **Save** to complete the application creation. This is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/efced05d75ad9843faca45ad5dca7fee.png)

<span id="cam"></span>
### Configuring CAM
> 
>- This step configures the trust relationship between OneLogin and Tencent Cloud.
> - In this example, the SAML identity provider and role name are both **test**.

1. In the [OneLogin Application Management page](https://xiaoyu.onelogin.com/apps), select the application **test** that you created.
2. Click **More Actions**. Select **SAML Metadata**, and download the IDP cloud data documentation. This is shown in the following figure.
![](https://main.qcloudimg.com/raw/56eb0b91f2dcf493478f1ae0e9d9c828.png)
3. Create the Tencent Cloud CAM identity provider and roles. For more information, see [Creating an IdP](https://intl.cloud.tencent.com/document/product/598/30391).

### Configuring OneLogin Single Sign-On
> This step maps OneLogin application attributes to Tencent Cloud attributes to create trust between the OneLogin application and Tencent Cloud.

1. In the [OneLogin Application Management page](https://xiaoyu.onelogin.com/apps), click the **test** application that has been created to redirect to the application editor page.
2. Select the **Configuration** tab, enter the following content, and then click **Save**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/89ba839089fe217aeedf1753010238ae.png)

>>
> - If your Tencent Cloud account is located on Tencent Cloud China website, perform configuration as follows:
SAML Consumer URL: https://cloud.tencent.com/login/saml
SAML Audience: https://cloud.tencent.com
SAML Recipient: https://cloud.tencent.com/login/saml
> - If your Tencent Cloud account is located on Tencent Cloud International website, perform configuration as follows:
SAML Consumer URL: https://intl.cloud.tencent.com/login/saml
SAML Audience: https://intl.cloud.tencent.com
SAML Recipient: https://intl.cloud.tencent.com/login/saml

3. Click **Parameters**, select **Add Parameter** and add the following two items.

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
		<td>Macro</td>
	<td>qcs::cam::uin/{AccountID}:roleName/{RoleName1};qcs::cam::uin/{AccountID}:roleName/{RoleName2},qcs::cam::uin/{AccountID}:saml-provider/{ProviderName}</td>
	</tr>
		<tr>
		<td>https://cloud.tencent.com/SAML/Attributes/RoleSessionName</td>
		<td>Include in SAML assertion</td>
		<td>Macro</td>
		<td>Test</td>
	</tr>
</table>


>> Replace {AccountID}, {RoleName}, and {ProviderName} of the **Role** source attribute with the following content:
>- {AccountID}: Replace this with your Tencent Cloud account ID. You can view this at [Account Information - Console](https://console.cloud.tencent.com/developer).
>- {RoleName}: Replace this with the role name you created on Tencent Cloud. You can view this at [Role - Console](https://console.cloud.tencent.com/cam/role).
>- {ProviderName}: Replace this with the SAML identity provider name that you created on Tencent Cloud. You can view this at [Identity Providers - Console](https://console.cloud.tencent.com/cam/idp).
>
4. Click **Save** on the upper right corner to save the configuration.

### Configuring OneLogin Users
1. Log in to [OneLogin User Management console](https://xiaoyu.onelogin.com/users).
2. Click **New User** to go to the user creation page.
3. <span id="step3"></span>Enter **First Name**, **Last Name**, **Email**, and **Username**, then click **Save User** to save. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/ef4f738c88f3c97fe5980286ad383ffa.png)

>Check your email for the password of this account, or click **More Actions** and select **Change Password** to change the password.
>
4. Click **Applications** in the user editing page. Select <image style="margin:0;" src="https://main.qcloudimg.com/raw/98a24d12696834b52f559d0abe490fd2.png"> on the right side. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/d8e9053d445b3af6d9aaecd74a0952b7.png)
5. In the dialog box that pops up, select the SAML **test** application that you created. Click **Continue**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/f7d3ecad4803cff72c62d665d4a2ec96.png)
6. In the editing page, click **Save**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/9d9389fbe5b821f23519524b30827c23.png)
7. Use the account created in [Step 3](#step3) to log in to OneLogin, and access the SAML **test** application created in the preceding sections. You will be redirected to the Tencent Cloud console.
