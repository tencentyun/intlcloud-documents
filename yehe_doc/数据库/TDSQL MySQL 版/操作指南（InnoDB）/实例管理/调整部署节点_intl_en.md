This document describes how to adjust deployed nodes in the TDSQL console. You can add replica nodes to enjoy cross-region replica support, reduce the execution pressure, and increase the read speed. You can also remove unnecessary replica nodes to save the redundant performance costs during idle hours.

>?
>- You can still use the old instance as usual during the adjustment.
>- The name, access IP, and access port of an instance will remain the same after the adjustment; however, the SQL passthrough ID (Setid) will change.
>- When the adjustment is completed, the database will be disconnected for several seconds. We recommend that you implement an automatic reconnection feature in your program.
>- During the adjustment, try avoiding operations such as modifying global parameters, instance name, or user password of the database.

## Adjusting the node deployment region
1. Log in to the [TDSQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql) and click the target instance ID in the instance list to enter the instance details page.
2. In **Availability Info** > **Deployment Mode** on the **Instance Details** page, click **Change Deployment Mode**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nYYT407_22.png)
3. On the **Change Deployment Mode** page, select the target deployment mode, and select the regions of the source and replica nodes in the drop-down lists.
>?**Target Deployment Mode**: You can select **Single-AZ** or **Multi-AZ**. In single-AZ mode, the region of replica nodes must be the same as that of the source node. In multi-AZ mode, replica nodes can be in any regions.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/cXE8735_23.png)

## Adding/Removing replica nodes
1. Log in to the [TDSQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql) and click the target instance ID in the instance list to enter the instance details page.
2. In **Availability Info** > **Deployment Mode** on the **Instance Details** page, click **Change Deployment Mode**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nQQH583_24.png)
3. On the **Change Deployment Mode** page, click **Add Replica Node** to add up to five replica nodes.
>?
>- **Delete**: Click it to remove existing replica nodes. If there is only one replica node, it cannot be removed.
>- **Scheduled switch**: You can choose to switch the database to its new configuration at a specified time, which is usually during off-peak hours and must be within 72 hours.
>- Generally, the switch time has a deviation of about 15 minutes, as there may be high amounts of write requests to large transactions, which will affect the data sync progress. In this case, the system will first guarantee sync between the new and old instances instead of performing the scheduled switch.
>- To ensure a successful switch, you can select the option for retry upon failure, and the system will try switching again two hours after a switch failure.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/KTQ9895_25.png)
