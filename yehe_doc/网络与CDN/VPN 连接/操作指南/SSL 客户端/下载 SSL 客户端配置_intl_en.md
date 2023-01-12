After successfully creating an SSL VPN client, you can download the client configuration for connecting to the SSL VPN server on the SSL VPN client management page. Two-way authentication will be performed when you use OpenVPN or a compatible VPN client to connect to the SSL VPN server through the downloaded client configuration. To guarantee your communication security, only after two-way authentication is passed can you access Tencent Cloud resources (such as CVM instances in a VPC) associated with the SSL VPN server gateway from the mobile client.

## Downloading the SSL VPN Client Configuration as a Tenant Admin
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **SSL VPN client** on the left sidebar.
3. Download the SSL VPN client configuration.
![]()
Click **Download the configuration** on the row of the target SSL VPN client certificate instance.
You need to distribute the downloaded configuration file to the user (such as an employee in your company) who needs to connect to Tencent Cloud through SSL VPN. This user must use the file to configure OpenVPN or a compatible VPN client in order to interconnect with the VPC. For detailed directions, see [Step 5: Configure the Mobile Client](https://intl.cloud.tencent.com/document/product/1037/43922).
>!Do not share the configuration file to unauthorized persons. If the configuration file is disclosed, disable the SSL VPN client promptly. For more information, see [Managing SSL VPN Client Certificate](https://intl.cloud.tencent.com/document/product/1037/43915).
>

## Downloading the SSL VPN Client Configuration on the Self-Service Portal[](id:Portal)
If identity verification is enabled when you create an SSL VPN server, the mobile client user (such as an employee in your company) can download the configuration file required by OpenVPN or a compatible VPN client on their own. In addition, Tencent Cloud uses an authentication mechanism to guarantee the security throughout the entire download process.

### Prerequisites
- The tenant admin has created a user group, added a user and granted the application access permission to the user group in the EIAM console. 
- The tenant admin has [created an SSL VPN server](https://intl.cloud.tencent.com/document/product/1037/43905) supporting identity verification in the VPC console.
- The tenant admin has distributed the ID of the SSL VPN server with identity verification enabled to you (as a user). If you don't have the ID, contact your admin to get it.


### Directions
The following steps are performed by a mobile client user (such as an employee of your enterprise) on their own:
1. Log in to the [Tencent Cloud Client VPN Self-Service Portal](https://self-service.vpnconnection.tencent.com/).
>?We recommend you use the latest version of Chrome.
>
  1. In the **SSL VPN server ID** input box, enter the ID distributed by the admin and click **Next** to access the login page.
![](https://qcloudimg.tencent-cloud.cn/raw/e62d6e75fbe70c168799a3534d86c9f3.png)
  2. Perform identity verification.      
Click ![](https://qcloudimg.tencent-cloud.cn/raw/6c78a80d3aadbade303cd3158eba47b9.png) to perform SAML authentication and click **Go to SAML** for login. You need to use the authentication method specified by your tenant admin. For example, if the admin specifies authentication by connecting to your enterprise account system in EIAM, you will see the domain account login page of your enterprise in the browser, and you need to enter your domain account for authentication. If the admin specifies another method such as WeCom, you need to enter the corresponding account for authentication.
>?
>1. Currently, login can be authenticated only through SAML. Make sure that you are in the EIAM user group associated with the SSL VPN access control policy. If "You are not authorized to access this application. Contact the admin." is displayed, you can contact the admin to add you to the EIAM user group.
>2. If you need to change the EIAM application, make sure that users in the original EIAM application have been moved to the new application for uninterrupted access.
>3. After the EIAM application switch, established SSL VPN connections won't be closed.
>
2. Download the SSL VPN client configuration file and client.
  1. In the **Download SSL VPN client configuration file** section, find the target configuration file and click **Download**.
  2. In the **Download SSL VPN client** section, download an appropriate SSL VPN client and install it.
![](https://qcloudimg.tencent-cloud.cn/raw/31bba25724ec755f717b7ecbd3c9aec6.png)
3. After installing the SSL VPN client, upload the downloaded configuration file. Then, the client will automatically connect to the SSL VPN server.
4. <img src="https://qcloudimg.tencent-cloud.cn/raw/b51ffdfba9caa56ccb742d2e60403d9a.png" width="35%">
