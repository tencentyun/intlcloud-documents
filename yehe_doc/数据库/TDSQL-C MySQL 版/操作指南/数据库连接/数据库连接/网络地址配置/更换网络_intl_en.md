This document describes how to change the network of TDSQL-C for MySQL in the console.

## Overview
TDSQL-C for MySQL supports VPC, which is capable of offering a diversity of smooth services. On this basis, it provides the cluster network change feature to help you manage network connectivity with ease.

## Notes
- When the network is changed, all of the cluster's private IPs are automatically replaced with new ones. You should modify the client program accordingly in time.
- You can specify the remaining validity period of the old IPs in the console. The period is 24 hours by default. If you set the period to 0 hours, the old IPs will be released immediately after the network is changed.
- The new VPC and subnet should be in the region of the cluster.

## Subnet description
A subnet is a logical network space in a VPC. You can create subnets in different AZs in the same VPC, which communicate with each other over the private network by default. Even if you select a subnet IP in another AZ in the region of the cluster, the network latency will not be increased because the actual business connection adopts nearby access.

## Directions
On the cluster management page, proceed according to the actually used view mode:
<dx-tabs>
::: Tab view
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Click the target cluster in the cluster list on the left to enter the cluster management page.
3. On the cluster management page, click **Change Network** after **Network**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/rtKz711_17.png)
4. In the **Change Network** pop-up window, select a network, set **Valid Hours of Old IPs**, and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/USUx520_18.png)
5. After changing the network, you can view the new network in the **Network** section on the cluster management page, and view the new private network address in the **Basic Info** section on the cluster details page.
:::
::: List view
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top and click the cluster ID in the cluster list or **Manage** in the **Operation** column to enter the cluster management page.
3. On the **Cluster Details** page, click **Change Network** in **Basic Info** > **Network**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/mDFf614_19.png)
4. In the **Change Network** pop-up window, select a network, set **Valid Hours of Old IPs**, and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/H4GX799_20.png)
5. After changing the network, you can view the new network in the **Network** section and the new private network address in the **Connection Info** section on the details page.
:::
</dx-tabs>





