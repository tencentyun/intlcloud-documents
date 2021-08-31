
The instance management feature displays the information of the TencentDB instances supporting DBbrain so that you can conveniently manage database instances.
- For TencentDB databases, this feature mainly displays the basic information of database instances (instance name/ID, status, etc.) and their groups, exception alarms, health scores, and operations.
- For external databases, this feature mainly displays the basic information of database instances (instance name/ID, status, etc.), exception alarms, health scores, monitoring data collection, slow log collection, access methods, agent status, instance status, accounts, and operations.

>?Currently, instance management is supported only for TencentDB for MySQL (excluding the basic single-node instance) and external MySQL databases.
>

## Instance Management List
### TencentDB databases 
Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/instance) and select **Instance Management** on the left sidebar. On the displayed page, select a TencentDB database at the top.

The instance management list shows the basic information of database instances, exception alarms, health scores, and operations. In the search box above the list, you can filter, aggregate, and search data by field.
- **Status**: this column displays whether database inspection or instance overview is enabled for an instance. To modify the status of an instance, click the **Edit** icon in the **Status** column; to modify the status of multiple instances at a time, select the instances in the list and click **Custom Settings** at the top. You can filter data by status.
- **Health Score**: this column displays the instance health score (the higher the score, the healthier the instance) rated during periodic health checks. You can sort data by health score.
- **Exception Alarm**: this column displays the number of exceptions of an instance detected by "24/7 Exception Diagnosis". You can click the number in the column to view more details and sort data by the number.
- **Group**: in this column, click the **Edit** icon to select the default group or create a group for an instance. You can also select one or multiple instances in the list and click **Manage Group** at the top to switch them to another group or add them to a new group.
- **Operation**: in this column, you can click **Performance Optimization** and enter the **Performance Optimization** page to view instance performance status.
![](https://main.qcloudimg.com/raw/3d4dcfd44e68c6b4a8223eedac65aa66.png)



## Custom Settings

DBbrain provides the custom settings feature. You can customize the settings about which instances to be displayed on the instance overview, database inspection or security governance page according to your needs.
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/monitor) and select **Instance Management** on the left sidebar. On the displayed page, select a database type at the top.
2. In the list, select one or multiple instances and click **Custom Settings**.
![](C:\Users\v_vwslwu\AppData\Roaming\Typora\typora-user-images\image-20210427163254193.png)
3. In the pop-up dialog box, enable or disable database inspection, instance overview or security governance. You can click **View Details** to view the basic information of the selected instance.
![](https://main.qcloudimg.com/raw/5f5b5b876b8e07b879911cc0577b8424.png)

