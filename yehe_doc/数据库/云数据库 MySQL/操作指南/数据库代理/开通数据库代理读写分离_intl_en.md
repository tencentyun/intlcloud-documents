
This document describes how to enable database proxy read/write separation in the TencentDB for MySQL console.

With the [database proxy read/write separation](https://intl.cloud.tencent.com/document/product/236/41093) feature, you can configure the database proxy address in your application so as to automatically forward write requests to the source instance and read requests to the read-only instance.

## Prerequisites
- You have [enabled database proxy](https://intl.cloud.tencent.com/document/product/236/41087).
- You have [created a read-only instance](https://intl.cloud.tencent.com/document/product/236/7270) for the source instance. If no read-only instances have been created, the feature enablement page will prompt you to purchase one.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, select a source instance with proxy enabled and click its ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Database Proxy** > **Read/Write Separation** > **Enable Now**.
![](https://main.qcloudimg.com/raw/b07508f045b727ca63c294b707159474.png)
3. In the displayed window, set configuration items such as **Remove Delayed RO Instances** and weight, and click **OK**.
>!
>- Only source and read-only instances that are in **Running** status can be added to the database proxy.
>- Currently, remote or delayed read-only instances cannot be mounted to the database proxy.
>
 - **Remove Delayed RO Instances**: specify whether to enable the removal policy. If a replication exception (such as replication delay or interruption) occurs on a read-only instance, the database proxy will remove the instance out of read/write separation temporarily. The delay threshold is 10 seconds by default, and at least 1 read-only instance should be retained.
 >?The set **Delay Threshold** and **Least RO Instances** take effect only for new connections.
 >
    - If the delay of a read-only instance exceeds the threshold, the instance will be removed, its weight will be automatically set to 0 after the removal, and the system will send an alarm to you (you should subscribe to the "removal of node mounted to database proxy" alarm first. For the configuration, please see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)).
    - The instance will be put back into the database proxy when its delay falls below the threshold. No matter whether delayed read-only instance removal is enabled, a read-only instance that is removed due to instance failure will rejoin the database proxy when it is repaired.
    - After **Least RO Instances** is set, if the database proxy finds that the number of read-only instances being routed is smaller than the set value, it will add exceptional read-only instances to read/write separation until the number of instances in read/write separation is greater than or equal to the set value.
Note: if a fatal failure (such as downtime) occurs on a read-only instance, it cannot be retained and counted into **Least RO Instances**.
 - **Assign Read Weight**: two weight assignment methods (automatic assignment by the system and custom assignment) are supported to configure the read weights of the source and read-only instances. The weight value must be an integer between 0 and 100.
 >?The configured read weight assignment takes effect immediately for all connections.
 >
    - The database proxy will assign read request traffic according to the set weights; for example, if weights of two read-only instances are 10 and 20 respectively, their read request traffic will be assigned at a ratio of 1:2.
    - The weight here refers to the read request weight only, as write requests are directly routed to the source database without participating in weight calculation; for example, if a client sends 10 write statements and 10 read statements, and the ratio of the source and read-only instance weights is 1:1, the source instance will receive 10 write statements and 5 read statements, and the read-only instance will receive 5 read statements only.
    - If you select **Assigned by system**, the system will automatically assign weights based on the instance's CPU and memory specification, and you can only set the weight of the source instance in this case.
    - If the weight of a read-only instance is 0, the database proxy will not connect to the instance. If its weight is changed from 0 to another value, the weight takes effect only for new connections.
 - **Failover**: we recommend you enable this parameter, so the database proxy can send read requests to the source instance if all read-only instances are exceptional.
 >?The configured failover capability takes effect only for new connections.
 >
If this parameter is disabled, when a read-only instance is exceptional, read requests will not be sent to the source instance (in order to prevent the source instance being affected by a high read load). However, all read requests will fail, after which the database proxy will proactively close the connection to the client.
 - **Apply to Newly Added RO Instances**: after this parameter is enabled, read-only instances created subsequently for the source instance will be automatically added to the database proxy.
![](https://main.qcloudimg.com/raw/f2eb858b2b37fd134913738b243a17e8.png)
4. After successfully enabling the read/write separation feature, you can view its basic information and architecture diagram and modify the relevant configuration items on the **Read/Write Separation** tab.
  - You can click **Modify** in the top-right corner to configure **Remove Delayed RO Instances**, assign weights, and modify other configuration items again.
  - You can click **Disable Read/Write Separation** in the top-right corner to disable read/write separation of the database proxy.
![](https://main.qcloudimg.com/raw/098c9fae971719881b6d20eee6ba0e73.png)
