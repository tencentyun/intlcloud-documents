## Overview
Okta is a solution provider for identification and access management. Tencent Cloud supports identity federation with Security Assertion Markup Language 2.0 (SAML 2.0). SAML 2.0 is an open standard used by many identity providers (IdPs). SAML 2.0-based federation can be used to integrate Okta with Tencent Cloud. Then, federated single sign-on (SSO) can be implemented by using an Okta account, and admins can authorize users that have their federated identity authenticated to log in to the Tencent Cloud console for resource management, eliminating the need to create a CAM sub-user for each employee in the organization.

## Directions
### <span id="stepCREATE"></span>Creating an Okta application
>?This step creates an Okta application. If you are already using one, skip this operation go straight to [configuring CAM](#stepCAM).

1. Log in to the [Okta website](https://www.okta.com), click your **username**, and select **Your Org** in the top-right corner as shown below:
![](https://main.qcloudimg.com/raw/29d6e0d2803dfe96284d9745571df382.png)
2. On the Okta homepage, click **Admin** in the top-right corner to enter the **Admin** page<span id="stepadmin"></span>.
3. On the **Admin** page, select **Applications** to go to the application management page<span id="stepapp"></span> as shown below:
![](https://main.qcloudimg.com/raw/5d55782d704ed50fac661603a30aa0d3.jpg)
4. On the application management page, click **Add Application**.
5. On the **Add Application** page, click **Create New App** as shown below:
![](https://main.qcloudimg.com/raw/c79f6042d72f01434555222f9e6079fd.png)
6. In the **Create a New Application Integration** pop-up window, select the platform, set the sign-on method to SAML 2.0, and click **Create** as shown below:
![](https://main.qcloudimg.com/raw/8126a0a697e4014e64138d7e8b0e5cab.png)
7. On the **General Settings** page, set **App name**, **App logo** (optional), and **App visibility** (optional) and click **Next**. This application can be used to integrate with Tencent Cloud to implement Okta SSO to the Tencent Cloud console for resource management.


### <span id="stepCAM"></span>Configuring SAML for the Okta application
>?
> - This step maps Okta application attributes to Tencent Cloud attributes to create trust between Okta and Tencent Cloud.
> -  If you followed the steps in [Creating an Okta application](#stepCREATE)  to create your application, you can go straight to [step 3](#stepbuzhou3).

1. Go to the [application management page](#stepapp), and click the name of the application you created.
2. On the **General** page, click **Edit** in the **SAML Settings** section, confirm the current **App name**, **App logo** (optional), and **App visibility** (optional), and click **Next** to enter the **Configure SAML** page.
3. <span id="buzhou3"></span>In the **Configure SAML** page, add the following information to **Single sign on URL** and **Audience URL(SP Entity ID)** under **GENERAL** as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/34ZI722_43a621945ad09042a40986abaea67962.png)
You can configure it based on the site of your Tencent Cloud account:
| Site | Single sign on URL| Audience URL(SP Entity ID) | 
|---------|---------|---------|
| Tencent Cloud International | https://www.tencentcloud.com/login/saml| www.tencentcloud.com|

4. In the **Configure SAML** page, add the following information to **ATTRIBUTE STATEMENTS** under **GENERAL** as shown below:
![](https://main.qcloudimg.com/raw/7114ab440ba1a593111296871fc807f9.png)
| Name | Name format | Value |
|---------|---------|---------|
| https://cloud.tencent.com/SAML/Attributes/Role | Unspecified| qcs::cam::uin/{AccountID}:roleName/{RoleName},qcs::cam::uin/{AccountID}:saml-provider/{ProviderName}
| https://cloud.tencent.com/SAML/Attributes/RoleSessionName | Unspecified| okta |
>? 
> Replace {AccountID}, {RoleName}, and {ProviderName} under **Value** with the following content:
>- {AccountID}: Replace this with your Tencent Cloud account ID. You can view this in [Account Information in the console](https://console.cloud.tencent.com/developer).
>- {RoleName}: Replace this with the role name you have created in Tencent Cloud for the IdP. For more information, see [Creating Role](https://intl.cloud.tencent.com/document/product/598/19381). Role names can be viewed in [Role in the console](https://console.cloud.tencent.com/cam/role). If you need to add more, you can add them in this format: qcs::cam::uin/{AccountID}:roleName/{RoleName}. Separate them by semicolons.
>- {ProviderName}: Replace this with the SAML IdP name that you created on Tencent Cloud. You can view this in [IdPs in the console](https://console.cloud.tencent.com/cam/idp).

5. Click **Next** to enter the **Feedback** page. Select the following information and click **Finish** to complete the CAM configuration as shown below:
![](https://main.qcloudimg.com/raw/a360cd597c75039a234b16608ca69e6c.png)

### Configuring SAML integration for the Okta application
>?This step configures the trust relationship between Okta and Tencent Cloud.

1. Log in to [Admin page](#stepadmin), and select **Applications** to go to the application management page.
2. On the application management page, click the name of the application you created to enter the application details page. Click **Sign On** as shown below:
![](https://main.qcloudimg.com/raw/3f43a5c67075b28f2ef649e93bfb9b8a.png)
3. On the **Sign On** page, click **Identity Provider metadata** to view the metadata of the IdP as shown below:
![](https://main.qcloudimg.com/raw/14e34ce4819d848c056fefa145b11060.png)
4. After obtaining the identity provider metadata, you can right click on the viewing page to save it locally.
5. Create the SAML identity provider and roles in Tencent Cloud. For more information, see [Creating IdP](https://intl.cloud.tencent.com/document/product/598/30391).


### Configuring an Okta user
>?This step assigns Tencent Cloud SSO access permissions to Okta users.

1. Log in to the [Admin page](#stepadmin) and click **Directory** > **People** to enter the user management page as shown below:
![](https://main.qcloudimg.com/raw/28eb0bceaebf2de3f073a72ed5bdd6c8.jpg)
2. On the user management page, click **Everyone** in the top-left corner. Locate the target user as shown below:
![](https://main.qcloudimg.com/raw/cc2022608165d39e0eeb3de495c5b07a.png)
3. Click the username to enter the user details page. Click **Assign Applications** in the top-left corner as shown below:
![](https://main.qcloudimg.com/raw/7ed74fd59d8d757dabcc2c82a7983582.png)
4. In the **Assign Applications** pop-up window, click **Done** to complete the configuration of the Okta user as shown below:
![](https://main.qcloudimg.com/raw/2d80e92964f5e7be9849c82ad4017ea7.jpg)
5. Go to the [application management page](#stepapp) , and click the name of the application you created to enter the application details page..
6. In the application details page, select **General**. Copy **Embed Link** under the **App Embed Link** box and log in to the Tencent Cloud console.

