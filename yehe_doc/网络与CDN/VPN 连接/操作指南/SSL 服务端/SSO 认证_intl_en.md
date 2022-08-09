If you download the SSL VPN client configuration on the [self-service portal](https://self-service-test.vpn.woa.com/), you can enable SSO authentication on the SSL VPN server.
>?Currently, the SSO authentication feature is in beta test and is available only in Singapore region. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>

## Prerequisites
You have created a user group, added a user, and granted the application access permission to the user group in the EIAM console.


## Enabling the feature while creating an SSL VPN server
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **SSL VPN server** on the left sidebar to enter the management page.
3. Click **Create**.
4. In the **Create an SSL VPN server** pop-up window, select **Certificate verification + Identity verification** for **Verification method** and select your EIAM application.
![](https://qcloudimg.tencent-cloud.cn/raw/6701e435810e93e5e4d1e64d0fb4ff99.png)
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
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
<td>Supported verification algorithms: SHA1 and MD5.</td>
</tr>
<tr>
<td>Encryption algorithm</td>
<td>Supported encryption algorithms: AES-128-CBC, AES-192-CBC, and AES-256-CBC</td>
</tr>
<tr>
<td>Compressed</td>
<td>No</td>
</tr>
<tr>
<td>Verification method</td>
<td><ul><li>Certificate verification: In this verification method, the SSL VPN server can be accessed through all SSL VPN client connections by default.</li><li>Certificate verification + Identity verification: In this verification method, only connections allowed by the access control policy can be established. You can configure the access control policy for specified user groups or all users. After this option is selected, you need to select an EIAM application.</li></ul></td>
</tr>
<tr>
<td>EIAM Application</td>
<td>An application created in the <a href="https://console.cloud.tencent.com/eiam">EIAM console</a>, which is used for access control.</td>
</tr>
<tr>
<td>Access control</td>
<td>SSL VPN server access control switch</td>
</tr>
</table>

5. You can **enable access control** as needed. For more information, see [Enabling Access Control](https://intl.cloud.tencent.com/document/product/1037/48814).

## Enabling the feature after creating an SSL VPN server
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **SSL VPN server** on the left sidebar to enter the management page.
3. Click the name of the target instance.
4. On the instance details page, click **Edit** in the **Server configurations** section on the **Basic information** tab.
5. Select **Certificate verification + Identity verification** for **Verification Method**, select an EIAM application, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/ed5d1a96b0b258b5c0a7294767ad1a6a.png)
