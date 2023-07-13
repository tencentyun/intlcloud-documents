In addition to the private network access, you can also connect to TDSQL-C for MySQL by using the system-assigned domain name and port after enabling the public network access. It takes about five minutes for the configuration to take effect. Note that the public network access should be used only for database development or management. For business access, you should use the private network access.

This document describes how to enable/disable public read-write and read-only addresses of a cluster in the console.

## Overview
A TDSQL-C for MySQL cluster contains read-write and read-only instances. They support both private and public network addresses, with the former enabled by default for you to access your instance over the private network and the latter enabled or disabled as needed. Note that the latter is automatically assigned by the system and cannot be customized currently.

>! 
>- After TDSQL-C for MySQL public network access is enabled, it will be controlled by the network access policies in the security group as described in [Creating and Managing TencentDB Security Groups](https://www.tencentcloud.com/document/product/1098/52007). You need to configure the corresponding policies in advance.
>- To access a cluster over the public network, you need to enable and configure a security group policy and **open the private network access port**; otherwise, public network access will fail.
>- Currently, the public network access feature is free of charge, but the stability of the public network bandwidth and traffic cannot be guaranteed.
>- The **Enable** button will be displayed for the public read-only address in the **Connection Info** section on the **Cluster Details** page only if there are read-only instances in your cluster.

## Supported regions
The public network address currently can be enabled for clusters in Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, Nanjing, Hong Kong (China), Singapore, Seoul, Tokyo, Silicon Valley, Frankfurt, and Virginia regions. It will be available in more regions in the future as displayed in the console.

## Enabling the public read-write/read-only addresses of a cluster
On the cluster management page, proceed according to the actually used view mode:
<dx-tabs>
::: Tab view
1. Log in to the [ TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), and click the target cluster in the cluster list on the left to enter the cluster management page.
2. In the cluster details, find the target instance and click **Enable** after the public network address in **Read-Write Address** or **Read-Only Address**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4Bwr893_19.png)
3. Then, the system will proceed based on the security group bound to the instance as follows:
**Case 1. The port is not opened in the current security group**
To enable public network access, you need to click **Authorize and Create**. The system will request for your authorization to automatically bind the security group with private network port (3306) enabled to the cluster, which facilitates the public network access. You can enter the security group page for subsequent settings or binding to another security group.
>!
>- The access port is not opened in your security group configuration. To ensure public network access, the system will automatically open the port for the cluster, and allow the access of "0.0.0.0/0" and "::/0". We recommend that you manually set it to a fixed IP for access.
>- After public network access is enabled, you can access TDSQL-C for MySQL through the domain name and port assigned by the system over the public network. The configuration takes effect in about 5 minutes.
>- You can only develop or help manage the database via public network. You must access your business over the private network.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/26kJ760_20.png)
**Case 2. The port is opened in the current security group**
In the pop-up window, read the note and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/NWGM631_21.png)
4. After public network access is enabled successfully, you can view the host and port in the public network address of the instance, which cannot be modified.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3Hgv027_22.png)
:::
::: List view
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click the ID of the target cluster in the cluster list to enter the cluster management page.
2. In the **Instance List** on the management page, select the target instance, click **Instance ID** or **Manage** in the operation column to enter the instance details page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/p7ES377_38.png)
3. On the **Instance Details** page, click **Enable** after **Connection Info* > **Public Read-Only Address**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QBZE513_39.png)
4. Then, the system will proceed based on the security group bound to the instance as follows:
**Case 1. The port is not opened in the current security group**
To enable public network access, you need to click **Authorize and Create**. The system will request for your authorization to automatically bind the security group with private network port (3306) enabled to the cluster, which facilitates the public network access. You can enter the security group page for subsequent settings or binding to another security group.
>!
>- The access port is not opened in your security group configuration. To ensure public network access, the system will automatically open the port for the cluster, and allow the access of "0.0.0.0/0" and "::/0". We recommend you manually set it to fixed IP access.
>- After public network access is enabled, you can access TDSQL-C for MySQL at the domain name and port assigned by the system over the public network. The configuration takes effect in about 5 minutes.
>- You can only develop or help manage the database via public network. You must access your business over the private network.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/tSSC602_40.png)
**Case 2. The port is opened in the current security group**
In the pop-up window, read the note and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/iZiD649_43.png)
5. After public network access is enabled successfully, you can view the host and port in the public network address in the **Connection Info** section, which cannot be modified.
:::
</dx-tabs>

## Disabling the public read-write/read-only addresses of a cluster
>!After the public network address is disabled, you cannot access the TDSQL-C for MySQL cluster over the public network at the domain name and port. Make sure that your system no longer uses the public network address to avoid unnecessary loss.
>
On the cluster management page, proceed according to the actually used view mode:
<dx-tabs>
::: Tab view
1. Log in to the [ TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), and click the target cluster in the cluster list on the left to enter the cluster management page.
2. In the cluster details, find the target instance and click **Disable** after the public network address.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/BK93318_42.png)
3. In the pop-up window, confirm that everything is correct and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/spea558_45.png)
:::
::: List view
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click the ID of the target cluster in the cluster list to enter the cluster management page.
2. In the **Instance List** on the cluster management page, select the target instance, click **Instance ID** or **Management** in the operation column to enter the instance details page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yAQN422_44.png)
3. On the **Instance Details** page, click **Enable** after **Connection Info* > **Public Read-Only Address**.
4. In the pop-up window, confirm that everything is correct and click **OK**.
:::
</dx-tabs>

