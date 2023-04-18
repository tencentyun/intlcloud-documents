This document describes how to change instance specifications in the TDSQL console. You can expand the capacity of specified shards by changing their node specifications to improve the business processing performance.

>?
>- You can still use the old instance as usual during the adjustment.
>- The name, access IP, and access port of an instance will remain the same after the adjustment; however, the SQL passthrough ID (Setid) will change.
>- When the adjustment is completed, the database will be disconnected for several seconds. We recommend that you implement an automatic reconnection feature in your program.
>- During the adjustment, try avoiding operations such as modifying global parameters, instance name, or user password of the database.

## Directions
1. Log in to the [TDSQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql) and click the target instance ID in the instance list to enter the instance details page.
2. In **Configuration Info** > **Configuration** on the instance details page, you can see the specification configuration of each node of the instance. Click **Adjust Configurations**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/K66T658_2.png)
3. On the **Shard Management** page, select a shard, click **Adjust Shard Configuration**, and select the target specification, disk capacity, and switch time.
>?**Scheduled switch**: You can choose to switch the database to its new configuration at a specified time, which is usually during off-peak hours and must be within 72 hours.
>- Generally, the switch time has a deviation of about 15 minutes, as there may be high amounts of write requests to large transactions, which will affect the data sync progress. In this case, the system will first guarantee sync between the new and old instances instead of performing the scheduled switch.
>- To ensure a successful switch, you can select the option for retry upon failure, and the system will try switching again two hours after a switch failure.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fhPB335_3.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/c5z5495_4.png)

## Billing overview
If you upgrade a database instance, the price difference between original and upgraded specifications is deducted from your account. If the account balance is insufficient, you need to top it up.

**Upgrade fees = (price of target specification - price of original specification) * remaining validity period**
