## Introduction
Okta is a solution provider for identification and access management. Tencent Cloud supports identity federation with SAML 2.0 (Security Assertion Markup Language 2.0). SAML 2.0 is an open standard used by many identity providers (IdPs). You can use the SAML 2.0-based identity federation to integrate Okta with Tencent Cloud, implementing single sign-on through the Okta account to log in to the Tencent Cloud console and manage Tencent Cloud resources without requiring the creation of a CAM sub-user for each employee of the enterprise or organization.

## Directions
### <span id="stepCREATE"></span>Creating Okta Applications
>This step creates an Okta application. If you're already using one, please skip this operation go straight to [configuring CAM](#stepCAM).
>
1. Log in to the [Okta website](https://www.okta.com), and click **User Name** > **Your Org** at the top right corner, as shown in the following figure:
![](https://main.qcloudimg.com/raw/29d6e0d2803dfe96284d9745571df382.png)
2. On the Okta home page, click **Admin** in the top right corner to go to the Admin interface<span id="stepadmin"></span>.
3. On the **Admin** page, select **Applications** to go to the application management page<span id="stepapp"></span>, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5d55782d704ed50fac661603a30aa0d3.jpg)
4. In the application management page, click **Add Application**.
5. In the **Add Application** page, click **Create New APP**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/c79f6042d72f01434555222f9e6079fd.png)
6. A **Create a New Application Integration** will pop up. Select the platform and set the sign-on method as SAML 2.0. Click **Create**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/8126a0a697e4014e64138d7e8b0e5cab.png)
7. In the **General Settings** page, add the **App name**, **App logo** (optional), and **App visibility** (optional) information and click **Next**. This application can be used to integrate with Tencent Cloud to implement Okta account single sign-on to the Tencent Cloud console to manage Tencent Cloud resources.


### <span id="stepCAM"></span>Configuring SAML for Okta Applications
>
> - This step maps Okta application attributes to Tencent Cloud attributes to create trust between Okta and Tencent Cloud.
> -  If you followed the steps in [Creating Okta Applications](#stepCREATE)  to create your application, you can go straight to [Step 3](#stepbuzhou3).

1. Go to the [application management page](#stepapp) , and click the name of the application you created.
2. In the **General** page, click **Edit** under the **SAML Settings** box. Confirm the current **App name**, **App logo** (optional), and **App visibility** (optional) information. Click **Next** to go to **Configure SAML** page.
3. <span id="buzhou3"></span>In the **Configure SAML** page, add the following information to **Single sign on URL** and **Audience URL(SP Entity ID)** under **GENERAL**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/43a621945ad09042a40986abaea67962.png)

>>
 - If your Tencent Cloud account is located on Tencent Cloud China website, perform configuration as follows:
 Single sign-on URL: https://cloud.tencent.com/login/saml
Audience URL (SP Entity ID): cloud.tencent.com
 > - If your Tencent Cloud account is located on Tencent Cloud International website, perform configuration as follows:
 Single sign-on URL: https://intl.cloud.tencent.com/login/saml
Audience URL (SP Entity ID): intl.cloud.tencent.com

4. In the **Configure SAML** page, add the following information to **ATTRIBUTE STATEMENTS** under **GENERAL**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/7114ab440ba1a593111296871fc807f9.png)

| Name | Name format | Value |
|---------|---------|---------|
| https://cloud.tencent.com/SAML/Attributes/Role | Unspecified| qcs::cam::uin/{AccountID}:roleName/{RoleName},qcs::cam::uin/{AccountID}:saml-provider/{ProviderName}
| https://cloud.tencent.com/SAML/Attributes/RoleSessionName | Unspecified| okta |

> 
> Replace {AccountID}, {RoleName}, and {ProviderName} under **Value** with the following content:
 - {AccountID}: Replace this with your Tencent Cloud account ID. You can view this at [Account Information - Console](https://console.cloud.tencent.com/developer).
 - {RoleName}: Replace this with the role name you have created in Tencent Cloud for the identity provider. For more information, see [Creating a Role](https://intl.cloud.tencent.com/document/product/598/19381). Role names can be viewed in [Role - Console](https://console.cloud.tencent.com/cam/role). If you need to add more, you can add them in this format: qcs::cam::uin/{AccountID}:roleName/{RoleName}. Separate them using semicolons (;).
 - {ProviderName}: Replace this with the SAML identity provider name that you created on Tencent Cloud. You can view this at [Identity Providers - Console](https://console.cloud.tencent.com/cam/idp).
>
5. Click **Next** to go to the **Feedback** page. Select the following information and click **Finish** to complete the CAM configuration. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/a360cd597c75039a234b16608ca69e6c.png)

### Configuring SAML Integration for Okta Applications
>This step configures the trust relationship between Okta and Tencent Cloud.
>
1. Log in to [Admin Interface](#stepadmin), and select **Applications** to go to the application management page.
2. In the application management page, click the name of the application you created to go to the application details page. Click **Sign On**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/3f43a5c67075b28f2ef649e93bfb9b8a.png)
3. On the **Sign On** page, click **Identity Provider Metadata** to view the metadata of the identity provider (IdP). This is shown in the following figure:
![](https://main.qcloudimg.com/raw/14e34ce4819d848c056fefa145b11060.png)
4. After obtaining the identity provider metadata, you can right click on the viewing page to save it locally.
5. Create the SAML identity provider and roles in Tencent Cloud. For more information, see [Creating an IdP](https://intl.cloud.tencent.com/document/product/598/30391).


### Configuring Okta Users
> This step assigns Tencent Cloud SSO access permissions to Okta users.
>
1. Log in to [Admin Interface](#stepadmin), click **People** under Directory to go to the user management page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/28eb0bceaebf2de3f073a72ed5bdd6c8.jpg)
2. In the user management page, click **Everyone** on the upper left corner. Locate the user for whom you need to configure permissions. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/cc2022608165d39e0eeb3de495c5b07a.png)
3. Click the user name to go to the user details page. Click **Assigned Applications** on the upper left corner. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/7ed74fd59d8d757dabcc2c82a7983582.png)
4. In the configurations window that pops up, click **Done** to complete the configuration of the Okta user. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/2d80e92964f5e7be9849c82ad4017ea7.jpg)
5. Go to the [application management page](#stepapp) , and click the name of the application you created to enter the application details page..
6. In the application details page, select **General**. Copy **Embed Link** under the **App Embed Link** box and log in to the Tencent Cloud console.
