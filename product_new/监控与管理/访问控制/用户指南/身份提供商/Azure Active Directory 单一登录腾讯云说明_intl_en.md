## Introduction

Azure Active Directory (Azure AD) is a cloud-based identity and access management service released by Microsoft. It can be used to help employees manage internal and external resources. Tencent Cloud supports identity federation with SAML 2.0 (Security Assertion Markup Language 2.0). SAML 2.0 is an open standard used by many identity providers (IdPs). You can use the SAML 2.0-based identity federation to integrate Azure Active Directory with Tencent Cloud, implementing single sign-on through the Azure AD account to log in to the Tencent Cloud console and manage Tencent Cloud resources without requiring the creation of a CAM sub-user for each employee of the enterprise or organization.

## Directions
### Creating Azure AD Enterprise Applications
>? This step creates an Azure AD enterprise application. If you’re already using one, you can skip this step and go straight to [configuring CAM](#stepCAM).


1. Go to the [Azure AD Portal](https://portal.azure.com/#home) and click **Azure Active Directory** in the left sidebar. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/1af5f2c6de562bb25d718c987d773a18.png)
2. Click **Enterprise Applications** and select **All Applications**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/83f279fe5afe68295750ef032f795878.png)
3. Click **New Application** to open the **Add Application** window. Select **Non-gallery Application**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/b4d7daa6d88d91b26070a914f9e02a8f.png)
4. Enter **Name** and click **Add** to complete the creation of the Azure AD application. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/c0cac58691701c27feefa7df9bb4fd81.png)

### <span id="stepCAM"></span>Configuring CAM
>? This step configures the trust relationship between Azure AD and Tencent Cloud to make them trust each other.
>
1. In the left sidebar, go to **Azure Active Directory** > **Enterprise Applications**, and select the application you created to go to the application overview page.
2. Click **Single Sign-On** to open the **Select a Single Sign-On Method** page.
3. In the **Select a Single Sign-On Method** page, select **SAML**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/b9b5f47f56a0f447e89495471f75d0ed.png)
4. In the **SAML Single Sign-On** preview page, download the **Federation Metadata XML** file under **SAML Signing Certificate**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/a394fe327b1e2456ce02195c75458005.png)
5. Create the SAML identity provider and roles in Tencent Cloud. For more information, see [Creating an IdP](https://intl.cloud.tencent.com/document/product/598/30391).

### Configuring the Azure AD Single Sign-On
>? This step maps Azure AD application attributes to Tencent Cloud attributes to create trust between the Azure AD application and Tencent Cloud.
>
1. In the **SAML Single Sign-On** overview interface, click <image style="margin:0;" src="https://main.qcloudimg.com/raw/836588594e0a214b5951ee5207fc2353.png"> on the upper right of **Basic SAML Configuration**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/87e30ebf37ae821062d9673100cae5ed.png)
2. In the **Basic SAML Configuration** editing page, enter the following information and click **Save**. This is shown in the following figure:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/e5is377_6d6cf16bc140940eabf61e5951809ed5.png)
You can configure it according to the site where your Tencent Cloud account is located
|Site |Identifier (entity ID)| Reply URL (Assertion Consumer Service (ACS) URL) | 
|---------|---------|---------|
| China website| cloud.tencent.com| https://cloud.tencent.com/login/saml|
| International website |www.tencentcloud.com| https://www.tencentcloud.com/login/saml|

3. In the **SAML Single Sign-On** overview interface, click <image style="margin:0;" src="https://main.qcloudimg.com/raw/836588594e0a214b5951ee5207fc2353.png"> in the upper right corner of **User Attributes and Claims** to open the **User Attributes and Claims editor. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/77dddf7d3248815f0483f33ef8bc6dea.png)
4. In the **User Attributes and Claims** editing page, click **Add New Claim** to go to the **Manage User Claims** page. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/8934abb7ff1b3972b319db12f455838a.png)
5. In the **Manage User Claims** page, add the following two claims, and click **Save**. This is shown in the following figure:

| Name | Namespace | Source | Source attribute |
|---------|---------|---------|---------|
|Role | https://cloud.tencent.com/SAML/Attributes | Attribute| qcs::cam::uin/{AccountID}:roleName/{RoleName},qcs::cam::uin/{AccountID}:saml-provider/{ProviderName} |
|RoleSessionName| https://cloud.tencent.com/SAML/Attributes | Attribute| Azure |

>? Replace {AccountID}, {RoleName}, and {ProviderName} of the **Role** source attribute with the following content:
>- {AccountID}: Replace this with your Tencent Cloud account ID. You can view this at [Account Information - Console](https://console.cloud.tencent.com/developer).
>- {RoleName}: Replace this with the role name you have created in Tencent Cloud for the identity provider. For more information, see [Creating a Role](https://intl.cloud.tencent.com/document/product/598/19381). Role names can be viewed in [Role - Console](https://console.cloud.tencent.com/cam/role). If you need to add more, you can add them in this format: qcs::cam::uin/{AccountID}:roleName/{RoleName}. Separate them using semicolons (;).
>- {ProviderName}: Replace this with the SAML identity provider name that you created on Tencent Cloud. You can view this at [Identity Providers - Console](https://console.cloud.tencent.com/cam/idp).
>
![](https://main.qcloudimg.com/raw/81d1de5875dcfe934c63a8e0f424253f.png)


### Configuring Azure AD Users
>? This step assigns Tencent Cloud SSO access permissions to Azure AD users.
>
1.Click **Azure Active Directory** in the left sidebar. Click **User** to open **All Users**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/1d5998772a8a2725454fb99edf9246da.png)
2. <span id="step2"></span>Click **New user** in the upper left corner. In the **User** page, enter **Name**, **User name**, and select**Show Password** to verify the password. Once the information is correct, click **Create** on the lower center to complete creation. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/db91a5689b7b1c46166c7ded9394a2a8.png)

>? The username format is as follows: Username@domain name. Usernames can be customized. Click **Azure Active Directory** in the left sidebar to open the overview page. You can view previously configured **Initial Domain Name** here. You can copy and save the username and password for future use.
>
3. In the left sidebar, go to **Azure Active Directory** > **Enterprise applications**, and select the application you created to go to the application overview page, and then click **Users and Groups**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/109c2e855804eec9cc4ded7556d450e6.png)
4. Click **Add User** to open **Users and Groups**. Select the user you created in [Step 2](#step2) and click the **Select** button. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/abfd66b0951aa34ed3f02266d8373975.png)
5. You will be redirected to the **Add Assignment** page. After confirming, click **Assign**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/edeab3a6fdfac2eb5e93bd106f21ae78.png)
6. In the left sidebar, go to **Azure Active Directory** > **Enterprise Applications**, and select the application you created to go to the application overview page.
7. Click **Single Sign-On** to open the **SAML Single Sign-On** overview page. Click **Test**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/82d9bf00d5a6c04d4c2b23b77e01ae26.png)
8. In the **Test Single Sign-on** page, select **Log in as Another User**.
9. Enter the username and password you saved in [Step 2](#step2) to log in to the Tencent Cloud console.
