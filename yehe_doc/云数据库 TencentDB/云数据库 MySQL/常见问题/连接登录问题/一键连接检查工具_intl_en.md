If you are unable to access a TencentDB for MySQL instance over the private or public network, you can use the connectivity checker to easily troubleshoot connectivity issues.

If you encounter a connectivity issue when accessing a TencentDB for MySQL instance from a CVM instance over the private or public network, you can use the connectivity check tool provided in the TencentDB for MySQL console to easily troubleshoot the issue.

## Private Network Connectivity Check
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click the ID of the instance to be checked and access the instance management page.
2. Select **Connection Check** > **Private Network Check**.
3. Click **Add CVMs that can access this instance**.
>?Only CVM instances in the same region as the TencentDB for MySQL instance are listed by default. If you need cross-region access, enable network interconnection through a [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
>
4. Click **Start Check** and a check report will be generated after the check is completed.
![](https://main.qcloudimg.com/raw/e233a1cd63718cfdc31347da83153fd8.png

5. In the **Operation** column of the check report, click **View Report** to view the check result.
 - If the check status is **Normal**, it means that the CVM instance is allowed to access this TencentDB for MySQL instance over the private network.
 - If the check status is **Abnormal**, it means that the CVM instance cannot access this TencentDB for MySQL instance over the private network. In this case, troubleshoot by following the **Handling Suggestions** and connect again.
<table>
<thead><tr><th>Check Item</th><th>Exception Handling</th></tr></thead>
<tbody><tr>
<td>MySQL instance status</td>
<td>The MySQL instance has been terminated. If it is terminated by mistake, please go to the <a href="https://console.cloud.tencent.com/mysql/recycle">recycle bin</a> to restore it.</td></tr>
<tr>
<td rowspan=2>CVM instance status</td>
<td>The CVM instance has been terminated. If it is terminated by mistake, please go to the <a href="https://console.cloud.tencent.com/cvm/recycler/cvm">recycle bin</a> to restore it.</td></tr>
<tr>
<td>The CVM instance is shut down. To use it, please start it up in the <a href="https://console.cloud.tencent.com/cvm/instance">CVM console</a>.</td></tr>
<tr>
<td rowspan=2>CVM and MySQL are in the same VPC</td>
<td>The networks of the CVM and MySQL instances are of different types. Please refer to <a href="https://intl.cloud.tencent.com/document/product/236/37864">Troubleshooting Connection Errors</a> to modify their network types so that they are in the same type of network.</td></tr>
<tr>
<td>The CVM and MySQL instances are using different VPC IP ranges. Please refer to <a href="https://intl.cloud.tencent.com/document/product/236/37864#wlwt">Troubleshooting Connection Errors</a> to modify their VPCs so that they are in the same VPC in the same region.</td></tr>
<tr>
<td>CVM security group policy</td>
<td>The <strong>outbound rule</strong> of the CVM instance's security group rejects the access to the IP and port of the MySQL instance. Please refer to <a href="https://intl.cloud.tencent.com/document/product/236/37864#caqzpzyw">Troubleshooting Connection Errors</a> to modify the outbound rule to allow the access to the IP and port of the MySQL instance.</td></tr>
<tr>
<td>MySQL security group policy</td>
<td>The <strong>inbound rule</strong> of the MySQL instance's security group rejects the access from the IP and port of the CVM instance. Please refer to <a href="https://intl.cloud.tencent.com/document/product/236/37864#maqzpzyw">Troubleshooting Connection Errors</a> to modify the inbound rule to allow the access from the IP and port of the CVM instance.</td></tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/b183b27af9c6b5a28cdb708f8a5c44d8.png">

## Public Network Connectivity Check
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click the ID of the instance to be checked and access the instance management page.
2. Select **Connection Check** > **Public Network Check**.
3. Click **Add an external server to access this instance**.
4. Click **Start Check** and a check report will be generated after the check is completed.
![](https://main.qcloudimg.com/raw/43d9e61c2052797740e7ef6817251f5e.png)
5. In the **Operation** column of the check report, click **View Report** to view the check result.
 - If the check status is **Normal**, it means that the server is allowed to access this TencentDB for MySQL instance over the public network.
 - If the check status is **Abnormal**, it means that the server cannot access this TencentDB for MySQL instance over the public network. In this case, troubleshoot by following the **Handling Suggestions** and connect again.
<table>
<thead><tr><th>Check Item</th><th>Exception Handling</th></tr></thead>
<tbody><tr>
<td>MySQL instance status</td><td>The MySQL instance has been terminated. If it is terminated by mistake, please go to the <a href="https://console.cloud.tencent.com/mysql/recycle">recycle bin</a> to restore it.</td></tr>
<tr>
<td>Public network access status</td>
<td>The public network access has been disabled for the MySQL instance. Please refer to <a href="https://intl.cloud.tencent.com/document/product/236/37788">Connecting to MySQL Instance</a> to enable it.</td></tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/01998fb06fe6d8a762dd5a2a9a5eb26c.png">
