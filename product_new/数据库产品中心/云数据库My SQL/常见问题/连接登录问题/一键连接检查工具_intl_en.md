
If you are unable to access a TencentDB for MySQL instance over the private or public network, you can use the connectivity checker to easily troubleshoot connectivity issues.

### Private Network Connectivity Check
If you encounter a connectivity issue when accessing a TencentDB for MySQL instance from a CVM instance over the private network, you can use the connectivity check tool provided in the TencentDB for MySQL Console to easily troubleshoot the issue.
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), select the instance to be troubleshot, and select the **Connectivity Check** tab on the instance management page.
2. When troubleshooting a private network connectivity issue, click **Add a CVM instance that accesses this instance** to add a CVM instance accessing this TencentDB for MySQL instance.
>Only CVM instances in the same region as the TencentDB for MySQL instance are listed by default. If you need cross-region access, enable network interconnection through a [peering connection](https://intl.cloud.tencent.com/document/product/215/5000).
>
![](https://main.qcloudimg.com/raw/e233a1cd63718cfdc31347da83153fd8.png)
3. After the addition, click **Start Check** and a check report will be generated after the check is completed.
![](https://main.qcloudimg.com/raw/0788aebb88c5509288e378dc1f541f22.png)
4. In the "Status" column of the check report, click **View Report** to view the check result.
 - If the check status is **Normal**, it means that the CVM instance is allowed to access this TencentDB for MySQL instance over the private network.
 - If the check status is **Exceptional**, it means that the CVM instance cannot access the TencentDB for MySQL instance over the private network. In this case, see the **Suggestion** in the exceptional check item for solution. For more information, see [FAQs About Instance Connectivity Issues](https://intl.cloud.tencent.com/document/product/236/31928).
![](https://main.qcloudimg.com/raw/b183b27af9c6b5a28cdb708f8a5c44d8.png)

### Public Network Connectivity Check
If you encounter a connectivity issue when accessing a TencentDB for MySQL instance from a server over the public network, you can use the connectivity checker provided in the TencentDB for MySQL Console to easily troubleshoot the issue.

1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), select the instance to be troubleshot, and select **Connectivity Check** > **Public Network Check** on the instance details page.
2. When troubleshooting a public network connectivity issue, click **Add a public network server that accesses this instance** to add a server accessing this TencentDB for MySQL instance.
3. After the addition, click **Start Check** and a check report will be generated after the check is completed.
![](https://main.qcloudimg.com/raw/43d9e61c2052797740e7ef6817251f5e.png)
4. In the "Status" column of the check report, click **View Report** to view the check result.
 - If the check status is **Normal**, it means that the server is allowed to access this TencentDB for MySQL instance over the public network.
 - If the check status is **Exceptional**, it means that the server cannot access the TencentDB for MySQL instance over the public network. In this case, see the **Suggestion** in the exceptional check item for solution. For more information, see [FAQs About Instance Connectivity Issues](https://intl.cloud.tencent.com/document/product/236/31928).
![](https://main.qcloudimg.com/raw/01998fb06fe6d8a762dd5a2a9a5eb26c.png)
