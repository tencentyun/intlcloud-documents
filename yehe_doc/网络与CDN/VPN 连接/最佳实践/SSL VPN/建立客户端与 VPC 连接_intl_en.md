This document describes how to connect to a VPC over an SSL VPN connection on a Windows, macOS, or Linux client.

## Background
This document takes the scenario below as an example to describe how to connect to a VPC over an SSL VPN connection on a Windows, macOS, or Linux client.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Wwus289_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230301163824.png)

## Configuration
The process of connecting to a VPC over an SSL VPN connection on the client is as follows:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EAnk058_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230301164021.png)

## Step 1: Create an SSL VPN Gateway
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Select **VPN Connections** > **VPN Gateway** on the left sidebar to enter the admin page.
3. Click **+New**.
4. In the **Create VPN gateway** pop-up window, configure the following gateway parameters.
<table>
<tr>
<th>Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Gateway name</td>
<td>Enter the VPN gateway name (up to 60 characters).</td>
</tr>
<tr>
<td>Region</td>
<td>Display the region of the VPN gateway.</td>
</tr>
<tr>
<td>AZ</td>
<td>Select the availability zone of the current gateway.</td>
</tr>
<tr>
<td>Protocol Type</td>
<td>Select <b>SSL</b>.</td>
</tr>
<tr>
<td>Bandwidth cap</td>
<td>Set a reasonable bandwidth cap for the VPN gateway according to the actual application scenarios.</td>
</tr>
<tr>
<td>Associated Network</td>
<td>Select <b>VPC</b>.</td>
</tr>
<tr>
<td>Network</td>
<td>Select the VPC associated with the VPN gateway</td>
</tr>
<tr>
<td>SSL VPN Connections</td>
<td>Select the number of clients that you want to connect. An SSL client allows connection from only one user.
</td>
</tr>
<tr>
<td>Billing Mode</td>
<td>The SSL VPN gateway is pay-as-you-go by default.</td>
</tr>
</table>

5. Click **Create**.

## Step 2. Create an SSL VPN Server[](id:step2)
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Select **VPN Connections** > **SSL VPN Server** on the left sidebar to enter the admin page.
>?A VPN gateway can be associated with only one SSL VPN server. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/1037/32682).
>
3. Click **+New**.
4. In the **Create an SSL VPN server** pop-up window, configure the following parameters.
<table>
<tr>
<th width="15%">Parameter</th>
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
<td>Enter the IP range that is assigned to the mobile client for communication. The IP range must not conflict with the VPC CIDR block of Tencent or your local IP range.</td>
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
</table>
5. Click **Create**.

## Step 3. Create an SSL VPN Client[](id:step3)
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Select **VPN Connections** > **SSL VPN Client** on the left sidebar to enter the admin page.
3. Click **+New**.
4. Configure the following parameters in the pop-up window.
5. Click **Create**. When **Certificate Status** changes to **Available**, the client is created.
6. On the SSL VPN client page, find the newly created client certificate and click **Download the configuration** in the **Operation** column.
>?An SSL client allows connection from only one user.
>

## Step 4. Configure a Route within the VPC
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Route Tables** on the left sidebar to enter the admin page.
3. In the list, click the ID of the target route table to enter its details page. You can also create a route table as instructed in [Creating Custom Route Tables](https://intl.cloud.tencent.com/document/product/215/35236).
4. Click **+ New routing policies**. In the pop-up window, configure the routing policy.
<table>
<tr>
<th>Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Destination</td>
<td>Enter the client IP range that is configured in <a href="#step2">Step 2: Create an SSL VPN Server</a>.</td>
</tr>
<tr>
<td>Next Hop Type</td>
<td>Select <b>VPN Gateway</b>.</td>
</tr>
<tr>
<td>Next Hop</td>
<td>Select an existing SSL VPN gateway.</td>
</tr>
</table>


## Step 5. Configure the Client
This section describes how to configure Windows, macOS, and Linux clients.


### Windows client
1. Download OpenVPN Connect for Windows from the OpenVPN website and install OpenVPN Connect.
![](https://qcloudimg.tencent-cloud.cn/raw/949a9e0031b880397bca986ac8eedfff.png)
2. Start OpenVPN Connect, select **Import Profile** > **FILE** to upload the SSL VPN client configuration file (.ovpn file) downloaded in [Step 3](#step3).
![](https://qcloudimg.tencent-cloud.cn/raw/f55cc9eebb56b47511a063eb1135556a.png)

### macOS client
1. Download OpenVPN Connect for macOS from the OpenVPN website and install OpenVPN Connect. 
![](https://qcloudimg.tencent-cloud.cn/raw/d08446a7176b855c0e19a77dd95cfdc3.png)
2. Start OpenVPN Connect, select **Import Profile** > **FILE** to upload the SSL VPN client configuration file (.ovpn file) downloaded in [Step 3](#step3).
![](https://qcloudimg.tencent-cloud.cn/raw/efade3f1b6290cae59a337e0927fe7c5.png)

### Linux client
1. Open the command line window.
2. Run the following command to install OpenVPN Connect.
CentOS distribution
```
yum install -y openvpn
```
Ubuntu distribution
```
sudo apt-get install openvpn
```
3. Extract the SSL VPN client certificate from the package downloaded in [step 3](#step3) and copy it to the `/etc/openvpn/conf/` directory.
4. Enter the `/etc/openvpn/conf/` directory and run the following command to establish a VPN connection:
```
openvpn --config /etc/openvpn/conf/config.ovpn --daemon
```

## Step 6. Test the Connectivity
After establishing the SSL VPN connection between Tencent Cloud and the client, you can use `ping` to test the connection.
For example, you can use the CVM in the VPC to `ping` an IP address in the client IP range. If the ping is successful, the VPC and the client can communicate with each other.
