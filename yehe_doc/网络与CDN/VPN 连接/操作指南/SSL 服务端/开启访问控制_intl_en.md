To guarantee your business security, SSL VPN provides the SSL VPN server access control feature to improve your linkage security.

## Notes
- If you enable access control, you need to configure the access policy after the server is created; otherwise, the server will reject all connections.
- If you select **Certificate verification** as the verification method, the SSL VPN server will accept all connections by default.
>?Currently, only SSO authentication-enabled SSL VPN servers support the access control feature. For more information, see [SSO Authentication](https://intl.cloud.tencent.com/document/product/1037/48813).
>

## Enabling access control while creating an SSL VPN server
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **SSL VPN server** on the left sidebar to enter the management page.
3. Click **+New**.
4. In the **Create an SSL VPN server** pop-up window, enable access control and configure relevant parameters while enabling identity verification.
>?If you enable access control, you need to [configure the access policy](https://intl.cloud.tencent.com/document/product/1037/48816) after the server is created; otherwise, the server will reject all connections.
>
![](https://qcloudimg.tencent-cloud.cn/raw/0f6f3db8d4fd7df53802dbd5b5335ee2.png)
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>Verification method</td>
<td><ul><li>Certificate verification: In this verification method, the SSL VPN server can be accessed through all SSL VPN client connections by default.</li><li>Certificate verification + Identity verification: In this verification method, only connections allowed by the access control policy can be established. You can configure the access control policy for specified user groups or all users. After this option is selected, you need to select an EIAM application.</li></ul></td>
</tr>
<tr>
<td>EIAM application</td>
<td>An application created in the <a href="https://console.cloud.tencent.com/eiam">EIAM console</a>, which is used for access control.</td>
</tr>
<tr>
<td>Access control</td>
<td>SSL VPN server access control switch</td>
</tr>
</table>


## Enabling access control after creating an SSL VPN server
>?If you enable access control, you need to configure the access policy after the server is created; otherwise, the server will reject all connections.
>
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **SSL VPN server** on the left sidebar to enter the management page.
3. Click the name of the target instance.
4. On the instance details page, **enable access control** in the **Server configurations** section on the **Basic information** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/d8178e07dc5d9310511bd218772a3fbb.png)
