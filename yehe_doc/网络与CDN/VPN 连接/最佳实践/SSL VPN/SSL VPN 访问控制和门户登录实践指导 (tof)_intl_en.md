This document describes how to use Employee Identity and Access Management (EIAM) and SSL VPN to implement access control to improve your business security.
>?
>- Currently, the SSO authentication feature is in beta testing and available only in the Singapore region. To use the feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>- The Tof SAML secret-free login portal **is accessible only to Tencent internal users**.
>

## Process
![](https://staticintl.cloudcachetci.com/yehe/backend-news/eivQ903_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230301163656.png)

## EIAM Verification Configuration
This section describes the main steps for configuring EIAM verification.

### Configuring the authentication source
>?
>1. Make sure that you have obtained your **metadata.xml** file from Tof SAML.
>2. If you encounter any issues, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
1. Log in to the EIAM console and click **Auth Source Management** on the left sidebar. On the **Authentication management** page that appears, click **Create authentication source**.
![](https://qcloudimg.tencent-cloud.cn/raw/a9a74b2cd910efde214f60c2c0260a1f.png)
2. Select **SAML** and click **Next** on the **Create authentication source** page.
<img  src="https://qcloudimg.tencent-cloud.cn/raw/031aad257dcc385b30510ea705cab0c7.png" width="80%"> 
3. Configure the authentication parameters on the **Edit authentication source information** tab.
<img  src="https://qcloudimg.tencent-cloud.cn/raw/d08d69104d5d8a80f930afec66d69f13.png" width="80%">  
 - Jump address: Set this parameter to the value of `<Location>` (the URL marked by **Tag1** in the image below) in `<SingleSignOnService></SingleSignOnService>` in the **metadata.xml** file.
 - Third party IDP certificate: Set this parameter to the value of `<X509Certificate>` (the certificate marked by **Tag2** in the image below) in `<KeyDescriptor use= "encryption"></KeyDescriptor>` in the **metadata.xml** file.
**Enable compression encoding**: Toggle on the switch.
![](https://qcloudimg.tencent-cloud.cn/raw/8114929da3a9dbcc13d4922dd2c9b11d.png)
4. Click **OK**. [](id:step4)
![](https://qcloudimg.tencent-cloud.cn/raw/02d38995680b280a2e05787e05ed6cad.png)
![](https://qcloudimg.tencent-cloud.cn/raw/16024f1ac5e4f2e5db0514b38ce636f1.png)
5. Click the SAML that is created in [Step 4](#step4) and then click **Download SAML metadata file**.[](id:step5)
![](https://qcloudimg.tencent-cloud.cn/raw/d493a30d9d37365c80d422aedb7f6e93.png)
6. Send the **metadata.xml** file that is downloaded in [Step 5](#step5) to **Tof Assistant** on WeCom for authorization.
After the authorization is complete, you can perform the subsequent steps.

### Creating a user
1. Log in to the EIAM console, select **User Management** > **Org Management** on the left sidebar and click **root**. On the page that appears, click **Create user**.
2. On the **Create user** page, configure the required parameters.
The username and password configured on this page are used to log in to the [Tencent Cloud Client VPN Self-Service Portal](https://self-service-test.vpn.woa.com/).


### Creating a user group and adding members
1. Select **User management** > **User group management** on the left sidebar. On the **User group management** page, click **Create user group**, configure the parameters, and click **OK**.
2. In the section of the created user group, click **Add user**.
3. On the **Add user** page that appears, add members to the user group and click **OK**.

### Creating an EIAM application
1. Select **App Management** on the left sidebar and click **Create through application marketplace**. Then select **OpenVPN** and click **Next: Edit application information**.
2. On the **Edit application information** tab, enter the relevant information as prompted and click **Next: Complete**.

### Authorizing the EIAM application
1. Select **App Authorization** on the left sidebar and then click **User group authorization** > **Add authorization**.
2. On the **Add Authorization** page, select the EIAM application just created and click **Next: Select user group**.
3. On the **Select user group** tab, select the user group to be authorized and click **Next: Complete**.

## SSL VPN Configuration

### Creating an SSL VPN gateway
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **VPN Connections** > **VPN gateway** on the left sidebar to enter the management page.
2. On the VPN gateway management page, click **+ New**. On the **Create VPN gateway** page, configure the SSL VPN gateway parameters.
3. Click **Create**.

### Creating an SSL VPN server
1. Select **VPN Connections** > **SSL VPN Server** on the left sidebar to enter the admin page.
2. On the SSL VPN server management page, click **+ New**. In the **Create an SSL VPN server** pop-up window, configure the SSL VPN server parameters.
<table>
<tr>
<th>Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Name</td>
<td>Enter the SSL VPN server name (up to 60 characters).</td>
</tr>
<tr>
<td>Region</td>
<td>Display the region of the SSL VPN server.</td>
</tr>
<tr>
<td>VPN gateway</td>
<td>Select an existing VPN gateway.</td>
</tr>
<tr>
<td>Server IP range</td>
<td>Tencent Cloud IP ranges accessed by mobile clients.</td>
</tr>
<tr>
<td>Client IP Range</td>
<td>Enter the IP range assigned to the mobile client for communication. The IP range shall not conflict with the VPC CIDR block of Tencent.</td>
</tr>
<tr>
<td>Protocol</td>
<td>Transmission protocol of the server.</td>
</tr>
<tr>
<td>Port</td>
<td>Enter the SSL VPN server port used for data forwarding.</td>
</tr>
<tr>
<td>Verification algorithm</td>
<td>Supported authentication algorithms: SHA1 and MD5.</td>
</tr>
<tr>
<td>Encryption algorithm</td>
<td>Supported encryption algorithms: AES-128-CBC, AES-192-CBC, and AES-256-CBC.</td>
</tr>
<tr>
<td>Compressed</td>
<td>No.</td>
</tr>
<tr>
<td>Access control</td>
<td><p>Enable it.
<dx-alert infotype="explain" title="">
To use this feature, please <a href="https://console.cloud.tencent.com/workorder/category"> submit a ticket</a> for application.
</dx-alert>
</td></tr>
<tr>
<td>Verification method</td>
<td>Select <b>Certificate verification + Identity verification</b>.</td>
</tr>
<tr>
<td>EIAM application</td>
<td>Select an application that is created in EIAM.</td>
</tr>
</table>


### Configuring an access control policy
1. Select **VPN Connections** > **SSL VPN Server** on the left sidebar to enter the admin page.
2. In the SSL VPN server list, click the ID of the target instance.
3. On the SSL VPN server details page, click **Access control** > **Add policy** and configure the policy information as prompted.
<table>
<tr>
<th>Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Destination</td>
<td>Enter the local IP range, that is, IP range for accessing the cloud.
<dx-alert infotype="explain" title="">
The destination IP range needs to be in the same IP range as the local IP range. If you change the local IP range, you need to modify the destination address of the access control.
</dx-alert>
</td>
</tr>
<tr>
<td>Access permission</td>
<td>Select <b>Specific user group</b>. After selecting this option, you need to configure the access group ID.</td>
</tr>
<tr>
<td>Access group ID</td>
<td>Select a user group to be granted the access permission.</td>
</tr>
<tr>
<td>Remarks</td>
<td>Enter the policy remarks, which are required and make it easier for you to find the policy.</td>
</tr>
</table>

4. Click **OK**.

### Creating an SSL VPN client
1. Select **VPN Connections** > **SSL VPN Client** on the left sidebar to enter the admin page.
2. In the **Create an SSL VPN client** pop-up window, specify a client name, select the SSL VPN server to which you want to connect, and click **OK**.


## Downloading an SSL VPN Client Configuration File and Client on the Client VPN Portal
1. Log in to the [Tencent Cloud Client VPN Self-Service Portal](https://self-service-test.vpn.woa.com/).
2. In the **SSL VPN server ID** input box, enter the ID of the created SSL VPN server and click **Next** to access the login page.
3. Log in to the Tencent Cloud Client VPN Self-Service Portal.
If you configured an authentication source in EIAM and added the authentication source to the user group that can access resources in the cloud, click <img src="https://qcloudimg.tencent-cloud.cn/raw/c62aaecd8068c405ad13294eb5f3971a.png" width="2%"> and then click **Jump to authentication (SAML)** to enter the page on which you can download the SSL VPN client configuration file and the SSL VPN client.
4. In the **Download SSL VPN client configuration file** section, find the target configuration file and click **Download**.
5. In the **Download SSL VPN client** section, find an appropriate SSL VPN client and click **Download**.
![](https://qcloudimg.tencent-cloud.cn/raw/47d85c50879a1617cfd9da6ad3d006f2.png)
This document takes macOS as an example. After you click **Download**, you will be redirected to the official website of OpenVPN, where you can download the client.


### Installing and connecting the SSL VPN client
1. Decompress the installation package locally and double-click the installer to install the client as prompted.
![](https://qcloudimg.tencent-cloud.cn/raw/64ef297dfdefeb11231d3ecb0c2ed5e1.png)
2. Upload the SSL VPN configuration file that you have downloaded.
After the configuration file is successfully uploaded, the client automatically connects to the SSL VPN server.
![](https://qcloudimg.tencent-cloud.cn/raw/89087fe374c6a4dc912518a0fad6bb18.png)
![](https://qcloudimg.tencent-cloud.cn/raw/4242b18feefb476f699e752533efa5f9.png)
![](https://qcloudimg.tencent-cloud.cn/raw/a63a8771ac2a538c97a690f6396639f5.png)

