This document describes how to use EIAM and SSL VPN to implement access control to improve your business security.
>?Currently, the SSO authentication feature is in beta test and is available only in Singapore region. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>

## Process
![](https://qcloudimg.tencent-cloud.cn/raw/3d9f258ad8024a35a0ab72766f30b58d.jpg)

## EIAM Verification Configuration
This section only describes the main steps of verification configuration in EIAM.

### Creating a user
1. Log in to the [EIAM console](https://console.cloud.tencent.com/eiam), select **User management** > **Organization management** > **Root node** on the left sidebar, and click **Create user**.
![](https://qcloudimg.tencent-cloud.cn/raw/d0b292c8b331b8f36eb300ed3778c5b8.png)
2. On the **Create user** page, configure the required parameters.
Here, the username and password will be used to log in to the [Tencent Cloud Client VPN Self-Service Portal](https://self-service-test.vpn.woa.com/).
![](https://qcloudimg.tencent-cloud.cn/raw/737dbcbd32db479589f1acba7a73df97.png)

### Creating a user group and adding the following members
1. Select **User management** > **User group management** on the left sidebar. On the **User group management** page, click **Create user group**, configure the parameters, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/633d6ea78a53edeb00968ba80243ed74.png)
2. In the section of the created user group, click **Add user**.
![](https://qcloudimg.tencent-cloud.cn/raw/90bc5ed0fb3975dfbede16809aa51b18.png)
3. On the **Add user** page, add members to the user group and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/c912be2bb043a563af9ae0252ed06b4c.png)

### Creating an EIAM application
1. Select **Application management** on the left sidebar and click **Create from Application Marketplace**. On the **Create from Application Marketplace** page, select **Tencent Cloud VPN** and click **Next: Edit application information**.
![](https://qcloudimg.tencent-cloud.cn/raw/9c95e0f1fd5d03da1ddcddd1c840bcd8.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0e1e299ec52779d5f80eec64de78f141.png)
2. On the **Edit application information** tab, enter the relevant information as prompted and click **Next: Complete**.
![](https://qcloudimg.tencent-cloud.cn/raw/5b573fb2b4e2f506548a7dbe3190d4d3.png)

### Granting permissions to the EIAM application
1. Select **Application authorization** on the left sidebar. On the **Application authorization** page, click **User group authorization** > **Add authorization**.
![](https://qcloudimg.tencent-cloud.cn/raw/373558137a62501312ea50d20d23dfc7.png)
2. On the **Add Authorization** page, select the EIAM application just created and click **Next: Select user group**.
![](https://qcloudimg.tencent-cloud.cn/raw/2ca01637c87b64911cf77d810cae663a.png)
3. On the **Select user group** tab, select the user group to be authorized and click **Next: Complete**.
![](https://qcloudimg.tencent-cloud.cn/raw/04c8349c5bd5fb846de58160ad51dc47.png)


## SSL VPN Configuration

### Creating an SSL VPN gateway
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **VPN Connections** > **VPN gateway** on the left sidebar to enter the management page.
2. On the VPN gateway management page, click **+ New**. On the **Create VPN gateway** page, configure the SSL VPN gateway parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/82738c5ab46577810286066ced03f5ae.png)
3. Click **Create**.

### Creating an SSL VPN server
1. Click **VPN Connections** > **SSL VPN server** on the left sidebar to enter the management page.
2. On the SSL VPN server management page, click **+ New**. In the **Create an SSL VPN server** pop-up window, configure the SSL VPN server parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/516cf8533fdf72c248d80eee40b503fc.png)
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>Name</td>
<td>Enter the SSL VPN server name (up to 60 characters).</td>
</tr>
<tr>
<td>Region</td>
<td>Select the region of the SSL VPN server.</td>
</tr>
<tr>
<td>VPN gateway</td>
<td>Select an existing VPN gateway.</td>
</tr>
<tr>
<td>Local IP address range</td>
<td>Tencent Cloud IP ranges accessed by mobile clients.</td>
</tr>
<tr>
<td>Client IP range</td>
<td>Enter the IP range assigned to the mobile client for communication. The IP range shall not conflict with the VPC CIDR block of Tencent.</td>
</tr>
<tr>
<td>Protocol</td>
<td>Transmission protocol of the server</td>
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
<td>No</td>
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
1. Click **VPN Connections** > **SSL VPN server** on the left sidebar to enter the management page.
2. In the SSL VPN server list, click the ID of the target instance.
3. On the SSL VPN server details page, click **Access control** > **Add policy** and configure the policy information as prompted.
![](https://qcloudimg.tencent-cloud.cn/raw/07420cb2280e0bd44947a8b6766fdc54.png)
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
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
<td>Notes</td>
<td>Enter the policy remarks, which are required and make it easier for you to find the policy.</td>
</tr>
</table>
4. Click **OK**.

### (Optional) Creating an SSL VPN client
>?To [download the SSL VPN client configuration](https://intl.cloud.tencent.com/document/product/1037/43914) and connect to the server, create an SSL VPN client as needed.
>
1. Click **VPN Connections** > **SSL VPN client** on the left sidebar to enter the management page.
2. In the **Create an SSL VPN client** pop-up window, set the client name, select the SSL VPN server to connect to, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/61410c7de573a258fa0c79a8ce5d0dea.png)

## Downloading an SSL VPN Client Configuration File and Client on the Client VPN Portal
1. Log in to the [Tencent Cloud Client VPN Self-Service Portal](https://self-service.vpnconnection.tencent.com).
2. In the **SSL VPN server ID** input box, enter the ID of the created SSL VPN server and click **Next** to access the login page.
![](https://qcloudimg.tencent-cloud.cn/raw/e62d6e75fbe70c168799a3534d86c9f3.png)
3. Log in to the Tencent Cloud Client VPN Self-Service Portal.
 - Login with account and password:
 Use the username and password set in EIAM for login.
 ![](https://qcloudimg.tencent-cloud.cn/raw/e94dbd40c28b390dd335de2739513369.png)
 - Automatic SAML authentication
 If you are in a user group in EIAM associated with an SSL VPN access control policy, you can directly click ![](https://qcloudimg.tencent-cloud.cn/raw/30a42799e4a89cef711771017807a9de.png) for SAML authentication and click **Go to SAML** for login.
 ![](https://qcloudimg.tencent-cloud.cn/raw/69a950e698da8532368ab5d3658f2f6a.png)
4. In the **Download SSL VPN client configuration file** section, find the target configuration file and click **Download**.
![](https://qcloudimg.tencent-cloud.cn/raw/31bba25724ec755f717b7ecbd3c9aec6.png)
5. In the **Download SSL VPN client** section, find an appropriate SSL VPN client and click **Download**.
This document takes macOS as an example. After you click **Download**, you will be redirected to the official website of OpenVPN, where you can download the client.
![](https://qcloudimg.tencent-cloud.cn/raw/a3acb588a5998f9f4ab26f6fae6f677e.png)

## SSL VPN Client Installation and Connection
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
6. The connection is established successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/3397478b0ae43da47d9c1711d60c828f.png)

