## Introduction
Azure Active Directory (Azure AD) is a cloud-based identity and access management service released by Microsoft. It can be used to help employees manage internal and external resources. Tencent Cloud supports identity federation with SAML 2.0 (Security Assertion Markup Language 2.0). SAML 2.0 is an open standard used by many identity providers (IdPs). You can use the SAML 2.0-based identity federation to integrate Azure Active Directory with Tencent Cloud, implementing single sign-on through the Azure AD account to log in to the Tencent Cloud console and manage Tencent Cloud resources without requiring the creation of a CAM sub-user for each employee of the enterprise or organization.

## Directions
### Creating Azure AD Enterprise Applications
>This step creates an Azure AD enterprise application. If you’re already using one, you can skip this step and go straight to [configuring CAM](#stepCAM).


1. Go to the [Azure AD Portal](https://portal.azure.com/#home) and click **Azure Active Directory** in the left sidebar. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/69bac51131949b7c9e471b5e1afdab86.png)
2. Click **Enterprise Applications** and select **All Applications**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/14c757580dd69950b7ce6352aaadcafc.png)
3. Click **New Application** to open the **Add Application** window. Select **Non-gallery Application**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/2612274fc991eaebaec4e102048b29fe.png)
4. Enter **Name** and click **Add** to complete the creation of the Azure AD application. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/94c765a2f385e47e641f9befbcb538bf.png)

### <span id="stepCAM"></span>Configuring CAM
> This step configures the trust relationship between Azure AD and Tencent Cloud to make them trust each other.
>
1. In the left sidebar, go to **Azure Active Directory** > **Enterprise Applications**, and select the application you created to go to the application overview page.
2. Click **Single Sign-On** to open the **Select a Single Sign-On Method** page.
3. In the **Select a Single Sign-On Method** page, select **SAML**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/103a22a9aed1c2a8f87f7c8fdcb38297.png)
4. In the **SAML Single Sign-On** preview page, download the **Federation Metadata XML** file under **SAML Signing Certificate**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/e14e13b4f0d8a6d376e71036ed3888f9.png)
5. Create the SAML identity provider and roles in Tencent Cloud. For more information, see [Creating an IdP](https://intl.cloud.tencent.com/document/product/598/30391).

### Configuring the Azure AD Single Sign-On
> This step maps Azure AD application attributes to Tencent Cloud attributes to create trust between the Azure AD application and Tencent Cloud.
>
1. In the **SAML Single Sign-On** overview interface, click <image style="margin:0;" src="https://main.qcloudimg.com/raw/836588594e0a214b5951ee5207fc2353.png"> on the upper right of **Basic SAML Configuration**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/abeffc5c30a39561448523a5fc29b8ee.png)
2. In the **Basic SAML Configuration** editing page, enter the following information and click **Save**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/a0161d7c8eeddcf00dab05d6a65dd2d7.png)

>>
> - If your Tencent Cloud account is located on Tencent Cloud China website, perform configuration as follows:
Identifier (entity ID): cloud.tencent.com
Reply URL (Assertion Consumer Service (ACS) URL): https://cloud.tencent.com/login/saml
> - If your Tencent Cloud account is located on Tencent Cloud International website, perform configuration as follows:
Identifier (entity ID): intl.cloud.tencent.com
Reply URL (Assertion Consumer Service (ACS) URL): https://intl.cloud.tencent.com/login/saml


3. In the **SAML Single Sign-On** overview interface, click <image style="margin:0;" src="https://main.qcloudimg.com/raw/836588594e0a214b5951ee5207fc2353.png"> in the upper right corner of **User Attributes and Claims** to open the **User Attributes and Claims editor. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/012441d7e961f9f784e05cc347c66294.png)
4. In the **User Attributes and Claims** editing page, click **Add New Claim** to go to the **Manage User Claims** page. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/4116fdd96ea5815f79db7c4aef508289.png)
5. In the **Manage User Claims** page, add the following two claims, and click **Save**. This is shown in the following figure:

| Name | Namespace | Source | Source attribute |
|---------|---------|---------|---------|
|Role | https://cloud.tencent.com/SAML/Attributes | Attribute| qcs::cam::uin/{AccountID}:roleName/{RoleName},qcs::cam::uin/{AccountID}:saml-provider/{ProviderName} |
|RoleSessionName| https://cloud.tencent.com/SAML/Attributes | Attribute| Azure |

> Replace {AccountID}, {RoleName}, and {ProviderName} of the **Role** source attribute with the following content:
>- {AccountID}: Replace this with your Tencent Cloud account ID. You can view this at [Account Information - Console](https://console.cloud.tencent.com/developer).
>- {RoleName}: Replace this with the role name you have created in Tencent Cloud for the identity provider. For more information, see [Creating a Role](https://intl.cloud.tencent.com/document/product/598/19381). Role names can be viewed in [Role - Console](https://console.cloud.tencent.com/cam/role). If you need to add more, you can add them in this format: qcs::cam::uin/{AccountID}:roleName/{RoleName}. Separate them using semicolons (;).
>- {ProviderName}: Replace this with the SAML identity provider name that you created on Tencent Cloud. You can view this at [Identity Providers - Console](https://console.cloud.tencent.com/cam/idp).
>
![](https://main.qcloudimg.com/raw/01b51dd563c366e82fc3f15ec31a5747.png)


### Configuring Azure AD Users
> This step assigns Tencent Cloud SSO access permissions to Azure AD users.
>
1.Click **Azure Active Directory** in the left sidebar. Click **User** to open **All Users**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/7ca36c24562a867451312e003c4afd25.png)
2. <span id="step2"></span>Click **New user** in the upper left corner. In the **User** page, enter **Name**, **User name**, and select **Show Password** to verify the password. Verify that the information is correct and click **Create** to complete creation. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/a67ec799cdcd060f34c86193f1e2ab7a.png)

> The username format is as follows: username@domain name. Usernames can be customized. Click **Azure Active Directory** in the left sidebar to open the overview page. You can view previously configured **Initial Domain Name** here. You can copy and save the username and password for future use.
>
3. In the left sidebar, go to **Azure Active Directory** > **Enterprise applications**, and select the application you created to go to the application overview page, and then click **Users and Groups**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/0fbc968bbdcdc1b1378e79a5e116d28a.png)
4. Click **Add User** to open **Users and Groups**. Select the user you created in [Step 2](#step2) and click the **Select** button. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/bd12f9c49ef1fd01bafc1d88566798e7.png)
5. You will be redirected to the **Add Assignment** page. After confirming, click **Assign**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/6e463c38b9bd16bb36b053f41550727d.png)
6. In the left sidebar, go to **Azure Active Directory** > **Enterprise Applications**, and select the application you created to go to the application overview page.
7. Click **Single Sign-On** to open the **SAML Single Sign-On** overview page. Click **Test**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/18869ef276217645b1ac03ab92ed3ab7.png)
8. In the **Test Single Sign-on** page, select **Log in as Another User**.
9. Enter the username and password you saved in [Step 2](#step2) to log in to the Tencent Cloud console.
