This document describes how to modify the private read-write/read-only addresses of TDSQL-C for MySQL in the console.

## Directions
On the cluster management page, proceed according to the actually used view mode:
<dx-tabs>
::: Tab view
1. Log in to the [ TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), and click the target cluster in the cluster list on the left to enter the cluster management page.
2. On the **Cluster Details** page, find the target instance and click ![](https://main.qcloudimg.com/raw/cf9bbcfaea10f0316bddd967cb6e8ffc.png) after its private network address.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/xUKU530_36.png)
3. In the pop-up window, modify the private network address and port and click **OK**.
>!Modifying the private network address affects the database business being accessed.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/jyRj398_37.png)
 - **Private Network Address**: You can customize the private network address within the available IP range.
 - **Custom Port**: You can customize the port in the range of 1024–65535.
 - **Valid Hours of Old IPs**: The default value is 24 hours, meaning that you can still access the instance at the old IP within 24 hours. You can customize the value between 0 and 168 hours. If you set the value to 0, the old IP will be repossessed immediately, and then you cannot access the instance at it.
:::
::: List view
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click the ID of the target cluster in the cluster list to enter the cluster management page.
2. Select the **Instance List** tab, select the target read-write or read-only instance, and click its ID to enter instance details page.
3. On the **Instance Details** page, click [](https://main.qcloudimg.com/raw/cf9bbcfaea10f0316bddd967cb6e8ffc.png) after the private network address in the **Connection Info** section.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/vW6D543_24.png)
3. In the pop-up window, modify the private network address and port and click **OK**.
>!Modifying the private network address affects the database business being accessed.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/VENv431_25.png)
 - **Private Network Address**: You can customize the private network address within the available IP range.
 - **Custom Port**: You can customize the port in the range of 1024–65535.
 - **Valid Hours of Old IPs**: The default value is 24 hours, meaning that you can still access the instance at the old IP within 24 hours. You can customize the value between 0 and 168 hours. If you set the value to 0, the old IP will be repossessed immediately, and then you cannot access the instance at it.
:::
</dx-tabs>



