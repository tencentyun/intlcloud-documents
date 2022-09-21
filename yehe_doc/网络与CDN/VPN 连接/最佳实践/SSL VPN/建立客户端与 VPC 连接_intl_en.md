This document describes how to connect to a VPC over an SSL VPN connection on a Windows, macOS, or Linux client.

## Background
This document takes the scenario below as an example to describe how to connect to a VPC over an SSL VPN connection on a Windows, macOS, or Linux client.
![](https://qcloudimg.tencent-cloud.cn/raw/e91b07b11273ad5cf40a610791f81599.jpg)

## Configuration
The process of connecting to a VPC over an SSL VPN connection on the client is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/2a6ce14b21ca082ea9a1dd5a0d23c9b3.jpg)

## Step 1. Create an SSL VPN Gateway
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. On the left sidebar, click **VPN Connections** > **VPN gateway** to enter the management page.
3. Click **+New**.
4. In the **Create VPN gateway** pop-up window, configure the following gateway parameters: </br><img src="" width="60%">
<table>
<tr>
<th>Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Gateway name</td>
<td>Enter the VPN gateway name (up to 60 characters)</td>
</tr>
<tr>
<td>Region</td>
<td>Display the region of the VPN gateway</td>
</tr>
<tr>
<td>AZ</td>
<td>Select the availability zone of the current gateway</td>
</tr>
<tr>
<td>Protocol Type</td>
    <td>Select <b>SSL</b></td>
</tr>
<tr>
<td>Bandwidth cap</td>
<td>Set a reasonable bandwidth cap for the VPN gateway according to the actual application scenarios</td>
</tr>
<tr>
<td>Associated Network</td>
    <td>Select <b>VPC</b></td>
</tr>
<tr>
<td>Network</td>
<td>Select the VPC associated with the VPN gateway</td>
</tr>
<tr>
<td>SSL VPN Connections</td>
<td>Number of client connections.</td>
</tr>
<tr>
<td>Billing Mode</td>
<td>The SSL VPN gateway is pay-as-you-go by default.</td>
</tr>
</table>

5. Click **Create**
![]()

## Step 2. Create an SSL VPN Server
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. On the left sidebar, click **VPN Connections** > **SSL VPN server** to enter the management page.
3. Click **+New**.
4. In the **Create an SSL VPN server** pop-up window, configure the following parameters: </br><img src="" width="60%">
<table>
<tr>
<th>Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Name</td>
<td>Enter the SSL VPN server name (up to 60 characters)</td>
</tr>
<tr>
<td>Region</td>
<td>Display the region of the SSL VPN server</td>
</tr>
<tr>
<td>VPN gateway</td>
<td>Select an existing VPN gateway</td>
</tr>
<tr>
<td>Server IP range</td>
<td>Tencent Cloud IP ranges accessed by mobile clients.</td>
</tr>
<tr>
<td>Client IP Range</td>
<td>Enter the IP range assigned to the mobile client for communication. The IP range shall not conflict with the VPC CIDR block of Tencent Cloud.</td></tr>
<tr>
<td>Protocol</td>
<td>Transmission protocol of the server</td>
</tr>
<tr>
<td>Port</td>
<td>Enter the SSL VPN server port used for data forwarding</td>
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
</table>
5. Click **Create**
![]()

## Step 3. Create an SSL VPN Client[](id:step3)
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. On the left sidebar, click **VPN Connections** > **SSL VPN client** to enter the management page.
3. Click **+New**.
4. In the **Create an SSL VPN client** pop-up window, configure the following parameters:
![]()
5. After configuring SSL VPN client parameters, click **OK**. When the certificate status becomes **Available**, the creation is completed.
6. On the SSL VPN client page, find the newly created client certificate and click **Download the configuration** in the **Operation** column.
![]()

## Step 4. Configure a Route within the VPC
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. On the left sidebar, click **Route table** to enter the management page.
3. In the list, click the ID of the target route table to enter its details page. You can also create a route table as instructed in [Creating Custom Route Tables](https://intl.cloud.tencent.com/document/product/215/35236).
4. Click **+ New routing policies**. In the pop-up window, configure the routing policy.
![]()
<table>
<tr>
<th>Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Destination</td>
<td>Enter the peer IP range configured when you created the SSL VPN server.</td>
</tr>
<tr>
<td>Next Hop Type</td>
    <td>Select <b>VPN gateway</b>.</td>
</tr>
<tr>
<td>Next Hop</td>
<td>Select a created SSL VPN gateway instance.</td>
</tr>
</table>


## Step 5. Configure the Client
This section describes how to configure Windows, macOS, and Linux clients.


### Windows client
1. Download OpenVPN Connect [here](https://openvpn.net/vpn-client/) and install it.
![](https://qcloudimg.tencent-cloud.cn/raw/949a9e0031b880397bca986ac8eedfff.png)
2. After the SSL VPN client is installed, select **Import Profile** > **FILE** to upload the SSL VPN client configuration file (.ovpn file) downloaded in [step 3](#step3).
![](https://qcloudimg.tencent-cloud.cn/raw/f55cc9eebb56b47511a063eb1135556a.png)

### macOS client
1. Download OpenVPN Connect [here](https://openvpn.net/vpn-client/) and install it. 
![](https://qcloudimg.tencent-cloud.cn/raw/d08446a7176b855c0e19a77dd95cfdc3.png)
2. After the SSL VPN client is installed, select **Import Profile** > **FILE** to upload the SSL VPN client configuration file (.ovpn file) downloaded in [step 3](#step3).
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
After establishing the SSL VPN connection between Tencent Cloud and the client, you can use `ping` to test it.
For example, you can use the CVM instance in the VPC to ping an IP address in the client IP range. If the ping succeeds, the VPC and the IDC can communicate with each other.
