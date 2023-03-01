This document describes how to use Employee Identity and Access Management (EIAM) and SSL VPN to implement access control to improve your business security.
>?Currently, the SSO authentication feature is in beta testing and is available only in the Singapore region. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>

## Process
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yYKL840_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230301163656.png)	

## EIAM Verification Configuration
This section describes the main steps for configuring EIAM verification.

### Creating a user
1. Log in to the [EIAM console](https://console.cloud.tencent.com/eiam), select **User management** > **Organization management** > **Root node** on the left sidebar, and click **Create user**.
2. On the **Create user** page, configure the required parameters.
The username and password configured on this page are used to log in to the [Tencent Cloud Client VPN Self-Service Portal](https://self-service.vpnconnection.tencent.com/).

### Creating a user group and adding members
1. Select **User management** > **User group management** on the left sidebar. On the **User group management** page, click **Create user group**, configure the parameters, and click **OK**.
2. In the section of the created user group, click **Add user**.
3. On the **Add user** page, add members to the user group and click **OK**.

### Creating an EIAM application
1. Select **Application management** on the left sidebar and click **Create from Application Marketplace**. On the **Create from Application Marketplace** page, select **Tencent Cloud VPN** and click **Next: Edit application information**.
2. On the **Edit application information** tab, enter the relevant information as prompted and click **Next: Complete**.

### Authorizing the EIAM application
1. Select **Application authorization** on the left sidebar. On the **Application authorization** page, click **User group authorization** > **Add authorization**.
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
<td>Enable it.
<dx-alert infotype="explain" title="">
If you want to try out this feature, contact Tencent Cloud technical support for application.
</dx-alert>
</td>
</tr>
<tr>
<td>Verification method</td>
<td>Select <b>Certificate verification + Identity verification</b>.</td>
</tr>
<tr>
<td>EIAM application</td>
<td>Select an application created in EIAM.</td>
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
<td>Enter the local IP range, i.e., IP range for accessing the cloud.
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

### (Optional) Creating an SSL VPN client
>?To [download the SSL VPN client configuration](https://intl.cloud.tencent.com/document/product/1037/43914) and connect to the server, create an SSL VPN client as needed.
>
1. Select **VPN Connections** > **SSL VPN Client** on the left sidebar to enter the admin page.
2. In the **Create an SSL VPN client** pop-up window, set the client name, select the SSL VPN server to connect to, and click **OK**.

## Downloading an SSL VPN Client Configuration File and Client on the Client VPN Portal
1. Log in to the [Tencent Cloud Client VPN Self-Service Portal](https://self-service.vpnconnection.tencent.com).
2. In the **SSL VPN server ID** input box, enter the ID of the created SSL VPN server and click **Next** to access the login page.
3. Log in to the Tencent Cloud Client VPN Self-Service Portal.
 Use the username and password that are created in EIAM to log in to the portal.
4. In the **Download SSL VPN client configuration file** section, find the target configuration file and click **Download**.
5. In the **Download SSL VPN client** section, find an appropriate SSL VPN client and click **Download**.
This document takes macOS as an example. After you click **Download**, you will be redirected to the official website of OpenVPN, where you can download the client.
![](https://qcloudimg.tencent-cloud.cn/raw/a3acb588a5998f9f4ab26f6fae6f677e.png)

## Installing and Connecting the SSL VPN Client
1. Decompress the installation package locally and double-click the installer to install the client as prompted.
![](https://qcloudimg.tencent-cloud.cn/raw/91055f2191fa4e39f9c0b3fc283d2555.png)
2. After the SSL VPN client is installed, select **Import Profile** > **FILE** to upload the downloaded SSL VPN client configuration file (.ovpn file).
![](https://qcloudimg.tencent-cloud.cn/raw/f39630923b2d06bc4b451e18a049e9a6.png)
3. After successful upload, select **CONNECT** for connection.
![](https://qcloudimg.tencent-cloud.cn/raw/2749df288279c6b7d9965b77a0621928.png)
4. Wait for the connection configured by the profile to be established.
![](https://qcloudimg.tencent-cloud.cn/raw/41ff2524ac4ffd107059cdd00c7ac246.png)
5. Verify the login information.
![](https://qcloudimg.tencent-cloud.cn/raw/d180678d03f8311ad6b7563a38b994d7.png)
6. The connection is successful.
![](https://qcloudimg.tencent-cloud.cn/raw/3397478b0ae43da47d9c1711d60c828f.png)
