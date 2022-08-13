
The instance management feature displays the information of the TencentDB instances supporting DBbrain so that you can conveniently manage database instances.
- For TencentDB databases, this feature mainly displays the basic information of database instances (instance name/ID, status, etc.) and their groups, exception alarms, health scores, and operations.
- For self-built databases, this feature mainly displays the basic information of database instances (instance name/ID, status, etc.), exception alarms, health scores, monitoring data collection, slow log collection, access mode, agent status, instance status, accounts, and operations.

>?Currently, this feature is supported only for TencentDB for MySQL (excluding basic single-node instances), TencentDB for Redis, TDSQL-C for MySQL, self-built MySQL, and TencentDB for MongoDB.
>

## Management List
### TencentDB databases 
Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/instance) and select **Instance Management** on the left sidebar. On the displayed page, select a TencentDB database at the top.

The instance management list shows the basic information of database instances, exception alarms, health scores, and operations. In the search box above the list, you can filter, aggregate, and search data by field.
- **Status**: This column displays whether database inspection or instance overview is enabled for an instance. To modify the status of an instance, click the **Edit** icon in the **Status** column; to modify the status of multiple instances at a time, select the instances in the list and click **Custom Settings** at the top. You can filter data by status.
- **Health Score**: This column displays the instance health score (the higher the score, the healthier the instance) rated during periodic health checks. You can sort data by health score.
- **Exception Alarms**: This column displays the number of exceptions of an instance detected by "24/7 Exception Diagnosis". You can click the number in the column to view more details and sort data by the number.
- **Group**: In this column, click the **Edit** icon to select the default group or create a group for an instance. You can also select one or multiple instances in the list and click **Manage Group** at the top to switch them to another group or add them to a new group.
>?Grouping is not supported for TDSQL-C for MySQL currently.
- **Operation**: In this column, you can click **Performance Optimization** to enter the corresponding feature details page and view the instance status.
![](https://main.qcloudimg.com/raw/e42c2a7be0056fdee2b1b161fbbc52fa.png)

### Self-built database
Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/instance) and select **Instance Management** on the left sidebar. On the displayed page, select a self-built database at the top.

The instance management list shows the basic information, exception alarms, health scores, monitoring data collection status, slow log collection status, access mode, Agent status, instance status, accounts, and operations of database instances. In the search box above the list, you can filter, aggregate, and search for data by field.
- **Status**: This column displays whether database inspection or instance overview is enabled for an instance. To modify the status of an instance, click the **Edit** icon in the **Status** column; to modify the status of multiple instances at a time, select the instances in the list and click **Custom Settings** at the top. You can filter data by status.
- **Health Score**: This column displays the instance health score (the higher the score, the healthier the instance) rated during periodic health checks. You can sort data by health score.
- **Exception Alarms**: This column displays the number of exceptions of an instance detected by "24/7 Exception Diagnosis". You can click the number in the column to view more details and sort data by the number.
- **Configuration**: This column displays the configuration of the database, including number of CPU cores, memory size, and disk size. The configuration is assigned by the server to the self-built database. DBbrain will configure the computing performance based on the entered values.
- **Monitoring and Collection**: This column displays whether the monitoring feature of DBbrain is enabled to collect the database performance data. The switch is toggled on by default and cannot be toggled off.
- **Slow Log Collection**: This column displays whether slow log collection is enabled. After the switch is toggled on, DBbrain will monitor the database's slow log status. Before this feature is enabled, you need to check whether the slow log collection permission is enabled. For more information, see [Slow Log Analysis Configuration](https://intl.cloud.tencent.com/document/product/1035/41701).
>?Self-built database instances that access the service through direct connection do not support slow log collection.
>
- **Network Type**: This column displays the network type of a connected self-built database instance, including private network and public network.
- **Access Mode**: This column displays the access method of a self-built database instance, including direct access and agent access.
- **Agent Status**: This column displays the real-time status of the Agent for a self-built database instance that accesses the service through the Agent. It helps you detect Agent exceptions promptly.
- **Instance Status**: This column displays the real-time status of a database instance, so you can promptly detect its exceptions.
- **Account**: This column displays the database account that is authorized to access the DBbrain service. You can click **Change Database Account** in the **Operation** column to change the authorized account.
- **Operation**:
  - Click **Performance Optimization** to enter the corresponding feature details page and view the instance status.
  - Select **More** > **Cancel Access** to remove the self-built database instance that accesses the DBbrain service.
  - Select **More** > **Change Database Account** to change the database account authorized to access the DBbrain service.
  - Select **More** > **Manage Agent** to view the basic information of the agent, including the agent's server IP, port, version, and status.
>?If an exception occurs on the Agent, click **Reconnect** in the **Operation** column next to the Agent status to restart the Agent. You can also click **Manual Restart Guide** in the top-right corner of the Agent management page to view how to manually restart the Agent on the server.
>
![](https://main.qcloudimg.com/raw/4a7a7a5d2ada6553eebc5f0fd72b7778.png)

## Custom Settings
DBbrain provides the custom settings feature. You can customize the settings about which instances to be displayed on the instance overview, database inspection or security governance page based on your needs.
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/instance) and select **Instance Management** on the left sidebar. On the displayed page, select a database at the top.
2. In the list, select one or multiple instances and click **Custom Settings**.
![](https://main.qcloudimg.com/raw/e56b342391a8b0be93611596df042f4c.png)
3. In the pop-up window, enable or disable database inspection or instance overview. You can click **View Details** to view the basic information of the selected instance.

