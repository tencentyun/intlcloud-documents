With the database proxy read/write separation feature, you can configure the database proxy address in your application, so that write requests are automatically forwarded to the read-write instance and read requests to each read-only instance.

This document describes how to enable/disable the read/write separation feature of TDSQL-C for MySQL.

## Prerequisite
- The instance is the read-write instance.
- You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://www.tencentcloud.com/document/product/1098/49999).
- You have created a read-only instance. For more information, see [Creating Read-Only Instance](https://intl.cloud.tencent.com/document/product/1098/40631).

## Enabling Read/Write Separation
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. Select the region at the top of the page and click the ID or **Manage** in the **Operation** column of the target cluster to enter the cluster management page.
3. On the **Database Proxy** tab on the cluster management page, select the **Read/Write Separation** tab and click **Enable Now**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fkYt458_8.png)
4. In the pop-up window, set the read/write configuration items and click **OK**.
>!
>- Only the running read-write instance and read-only instances can be added to the database proxy.
>- Currently, remote or delayed read-only instances cannot be mounted to the database proxy.
>
   - **Consistency Settings**: Three consistency levels are available, that is, eventual consistency, session consistency, and global consistency.
   - **Assign Read Weight**: Assign read weights to instances. You can select **Assigned by system** or **Custom**. Each weight must be an integer between 0 and 100. The configured read weight assignment takes effect immediately for all connections.
     - The database proxy will assign read request traffic according to the set weights; for example, if weights of two read-only instances are 10 and 20 respectively, their read request traffic will be assigned at a ratio of 1:2.
     - The weight here refers to the read request weight only, as write requests are directly routed to the source database without participating in weight calculation; for example, if a client sends 10 write statements and 10 read statements, and the ratio of the source and read-only instance weights is 1:1, the read-write instance will receive 10 write statements and 5 read statements, and the read-only instance will receive 5 read statements only.
     - If you select **Assigned by system**, the system will automatically assign weights based on the instance's CPU and memory specification, and you can only set the weight of the read-write instance in this case.
     - If the weight of a read-only instance is 0, the database proxy will not connect to the instance. If its weight is changed from 0 to another value, the weight takes effect only for new connections.
   - **Failover**: Specifies whether to enable failover. We recommend you enable this option, so the database proxy can send read requests to the read-write instance if all read-only instances are exceptional.
>?The configured failover capability takes effect only for new connections.
   - **Apply to Newly Added RO Instances**: Enable or disable this parameter. After it is enabled, if you purchase new read-only instances, they will be automatically added to the database proxy.
     - If **Assign Read Weight** is set to **Assigned by system**, newly purchased read-only instances will be assigned with the default weight based on their specification.
     - If **Assign Read Weight** is set to **Custom**, when newly purchased read-only instances are added to the RO group, their weights will be 0 by default, which can be modified in the configuration of the database proxy's read/write separation.
      ![](https://staticintl.cloudcachetci.com/yehe/backend-news/yEh4331_9.png)

## Page display
After the database proxy's read/write separation feature is enabled, on the **Read/Write Separation** tab, you can view the basic information and read/write separation architecture diagram. You can also click buttons on the right to adjust the configuration and disable the feature.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Rsey396_10.png)

## Disabling Read/Write Separation
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. Select the region at the top of the page and click the ID or **Manage** in the **Operation** column of the target cluster to enter the cluster management page.
3. On the **Database Proxy** tab on the cluster management page, select the **Read/Write Separation** tab and click **Disable Read/Write Separation** on the right.

