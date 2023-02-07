In addition to the private network access, you can also connect to TDSQL-C for MySQL by using the system-assigned domain name and port after enabling the public network access. It takes about five minutes for the configuration to take effect. Note that the public network access should be used only for database development or management. For business access, you should use the private network access.

This document describes how to enable/disable public read-write and read-only addresses of a cluster in the console.

## Overview
A TDSQL-C for MySQL cluster contains read-write and read-only instances. They support both private and public network addresses, with the former enabled by default for you to access your instance over the private network and the latter enabled or disabled as needed. Note that the latter is automatically assigned by the system and cannot be customized currently.

>! 
>- After TDSQL-C for MySQL public network access is enabled, it will be controlled by the network access policies in the [security group](https://www.tencentcloud.com/document/product/1098/52007). You need to configure the corresponding policies in advance.
>- To access a cluster over the public network, you need to enable and configure a security group policy and **open the private network access port**; otherwise, public network access will fail.
>- Currently, the public network access feature is free of charge, but the stability of the public network bandwidth and traffic cannot be guaranteed.
>- The **Enable** button will be displayed for the public read-only address in the **Connection Info** section on the **Cluster Details** page only if there are read-only instances in your cluster.

## Enabling the public read-write/read-only addresses of a cluster
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click the ID of the target cluster in the cluster list to enter the cluster management page.
2. On the **Cluster Details** page, click **Enable** after the target public network address.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4ZXJ420_2.png)
3. In the pop-up window, confirm that everything is correct and click **OK**.

## Disabling the public read-write/read-only addresses of a cluster
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click the ID of the target cluster in the cluster list to enter the cluster management page.
2. On the **Cluster Details** page, click **Disable** after the target public network address.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4tVY503_3.png)
3. In the pop-up window, confirm that everything is correct and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/rBZL349_4.png)
