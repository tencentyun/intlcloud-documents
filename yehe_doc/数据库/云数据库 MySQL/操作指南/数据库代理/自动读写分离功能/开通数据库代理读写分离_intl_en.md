With the database proxy read/write separation feature, you can configure the database proxy address in your application to automatically forward write requests to the source instance and read requests to the read-only instance. For more information, see [Automatic Read/Write Separation Overview](https://intl.cloud.tencent.com/document/product/236/42050).

This document describes how to enable/disable the read/write separation feature of TencentDB for MySQL.

## Prerequisites
- The instance is the source instance.
- You have [enabled the database proxy](https://intl.cloud.tencent.com/document/product/236/42052) for the instance.
- You have [created a read-only instance](https://intl.cloud.tencent.com/document/product/236/7270) for the instance.

## Enabling read/write separation
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
2. Select the region at the top of the page and click the ID or **Manage** in the **Operation** column of the target instance to enter the instance management page.
3. On the **Database Proxy** tab on the instance management page, select the **Read/Write Separation** tab and click **Enable Now**.
![](https://main.qcloudimg.com/raw/b07508f045b727ca63c294b707159474.png)
4. In the pop-up window, set the relevant configuration items and click **OK**.
>!
>- Only source and read-only instances that are in **Running** status can be added to the database proxy.
>- Currently, remote or delayed read-only instances cannot be mounted to the database proxy.
>
   - **Remove Delayed RO Instances**: Specify whether to enable the removal policy. If a replication exception (such as replication delay or interruption) occurs on a read-only instance, the database proxy will remove the instance out of read/write separation temporarily. The delay threshold is ten seconds by default, and at least one read-only instance should be retained.
>?The set **Delay Threshold** and **Least RO Instances** take effect only for new connections.
   - **Delay Threshold**: Specify the maximum delay allowed when a read-only instance syncs data from the source instance. If the delay of a read-only instance exceeds this threshold, read requests will not be forwarded to it, regardless of its weight. The value must be an integer greater than or equal to 1.
     - If the delay of a read-only instance exceeds the threshold, the instance will be removed, its weight will be automatically set to 0 after the removal, and the system will send an alarm to you (you should subscribe to the "removal of node mounted to database proxy" alarm first. For the configuration, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)).
     - The instance will be put back into the database proxy when its delay falls below the threshold. No matter whether delayed read-only instance removal is enabled, a read-only instance that is removed due to instance failure will rejoin the database proxy when it is repaired.
     - After **Least RO Instances** is set, if the database proxy finds that the number of read-only instances being routed is smaller than the set value, it will add abnormal read-only instances to read/write separation until the number of instances in read/write separation is greater than or equal to the set value.
>   !If a fatal failure (such as downtime) occurs on a read-only instance, it cannot be retained and counted into **Least RO Instances**.
   - **Least RO Instances**: This is the minimum number of instances that should be retained in the RO group. When there are fewer instances in the RO group, even if an instance exceeds the delay threshold, it will not be removed.
   - **Assign Read Weight**: Assign read weights to instances. You can select **Assigned by system** or **Custom**. Each weight must be an integer between 0 and 100.
    - For database proxy versions earlier than v1.3.1, if the weight of a read-only instance is 0, the database proxy will not connect to the instance. If its weight is changed from 0 to another value, the weight takes effect only for new connections.
    - For database proxy versions v1.3.1 and later, if the weights of all the read-only instances available at the specified connection address are 0, the database proxy will increase all such weights to 1 by default to ensure that there will still be read-only nodes available when an exception occurs.
   - **Failover**: Set whether to enable failover. After it is enabled, when database connection fails due to a database proxy failure, the access address of the database proxy will be connected to the source instance for access. When the database proxy recovers, it will be connected back to the database proxy again.
>?The configured failover capability takes effect only for new connections.
   - **Apply to Newly Added RO Instances**: Enable or disable this parameter. After it is enabled, if you purchase new read-only instances, they will be automatically added to the database proxy.
     - If **Assign Read Weight** is set to **Assigned by system**, newly purchased read-only instances will be assigned with the default weight based on their specification.
     - If **Assign Read Weight** is set to **Custom**, when newly purchased read-only instances are added to the RO group, their weights will be 0 by default, which can be modified in the configuration of the database proxy's read/write separation.
   ![](https://main.qcloudimg.com/raw/f2eb858b2b37fd134913738b243a17e8.png)

## Page display
After the database proxy's read/write separation feature is enabled, on the **Read/Write Separation** tab, you can view the basic information and read/write separation architecture diagram. You can also click buttons on the right to adjust the configuration and disable the feature.
![](https://main.qcloudimg.com/raw/098c9fae971719881b6d20eee6ba0e73.png)

## Disabling read/write separation
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
2. Select the region at the top of the page and click the ID or **Manage** in the **Operation** column of the target instance to enter the instance management page.
3. On the **Database Proxy** tab on the instance management page, select the **Read/Write Separation** tab and click **Disable Read/Write Separation** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/efa07dc1350c2fc9dc878914e22aef05.png)
