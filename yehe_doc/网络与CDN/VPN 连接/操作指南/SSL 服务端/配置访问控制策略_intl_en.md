To guarantee your business security, SSL VPN provides the SSL VPN server access control feature for you to manage your SSL VPN servers in a fine-grained manner.
>?Currently, only SSO authentication-enabled SSL VPN servers support the access control feature. For more information, see [SSO Authentication](https://intl.cloud.tencent.com/document/product/1037/48813).
>

## Prerequisites
- You have created a user group, added a user, and granted the application access permission to the user group in the [EIAM console](https://console.cloud.tencent.com/eiam).
- You have enabled certificate verification + identity verification and access control for the SSL VPN server in the [VPC console](https://console.cloud.tencent.com/vpc/vpn-ssl-server?rid=1).
  - Option 1. Enable the feature while creating an SSL VPN server.
![](https://qcloudimg.tencent-cloud.cn/raw/5f32dd99ac9a8c4ab930916557ff5f79.png)
  - Option 2. Enable the feature after creating an SSL VPN server.
![](https://qcloudimg.tencent-cloud.cn/raw/eef0500174f5f17592c7a36b86aaa340.png)
>!
>- If you select **Certificate verification** as the verification method, the SSL VPN server can be accessed through all client connections by default, that is, any client can connect to it.
>- If you enable access control, you need to configure the access policy after the SSL VPN server is created; otherwise, the server will reject all connections.
>

## Configuring an access control policy
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **SSL VPN server** on the left sidebar to enter the management page.
3. Click the name of the target instance.
![]()
4. On the instance details page, click **Access control** > **Add policy**.
![](https://qcloudimg.tencent-cloud.cn/raw/fb46b6a30b3166f1a152c549d684c1d3.png)
5. In the pop-up window, configure an access control policy.
![](https://qcloudimg.tencent-cloud.cn/raw/077c3f08806bdd239166584bf4113ae4.png)
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
<td>
<ul>
<li>Specific user group: The access control policy will take effect for the specified user group, and you need to configure the access group ID after selecting this option.</li>
<li>All users: The access control policy will take effect for all users.</li>
</ul>
<dx-alert infotype="explain" title="">
You can choose to configure access policies for specific user groups or all users. Specific user groups can be user groups configured on the [identity verification platform](https://console.cloud.tencent.com/eiam).
</dx-alert>
</td>
</tr>
<tr>
<td>Access group ID</td>
<td>An access group ID is the ID of a user group in the EIAM application. You can select multiple IDs, and then the access control policy will take effect only for the selected user groups.</td>
</tr>
<tr>
<td>Notes</td>
<td>Enter the policy remarks, which are required and make it easier for you to find the policy.</td>
</tr>
</table>
6. Click **OK**.
After completing the configuration, the SSL VPN server will accept all connections from users in the user group.

## Deleting an access control policy
>!
>- After an access control policy is deleted, clients of users in user groups associated with the policy cannot access the SSL VPN server.
>- If all access control policies are deleted, the SSL VPN server will reject the access requests from all clients by default. If you want the server to be accessible again, you can configure an access control policy or change the verification method to **Certificate verification**.
>
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **SSL VPN server** on the left sidebar to enter the management page.
3. Click the name of the target instance and delete the target policy on the **Access control** tab.
  - Delete multiple policies: Select policies to be deleted in the policy list and click **Batch delete**.
  - Delete one policy: Click **Delete** in the **Operation** column of the policy to be deleted.
4. In the pop-up window, click **OK**.

## Editing an access control policy
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **SSL VPN server** on the left sidebar to enter the management page.
3. Click the name of the target instance. On the **Access control** tab, click **Edit** in the **Operation** column of the target policy and modify its parameters as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/dbd17b3ec4f644b15b311f462111f08c.png)
4. Click **OK**.
