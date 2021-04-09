The instance management feature displays the information of the TencentDB instances supporting DBbrain. It mainly shows the basic information of database instances (instance name/ID, status, etc.) and their access sources, groups, exception alarms, health scores, and operations.
>?Currently, instance management is supported only for TencentDB for MySQL (excluding the basic single-node instance).
>


## Instance Management List
Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/instance) and select **Instance Management** on the left sidebar. On the displayed page, select a database type at the top.

The instance management list shows the basic information of database instances and their access sources, exception alarms, health scores, and operations. In the search box above the list, you can filter, aggregate, and search data by field.
- **Status**: this column displays whether database inspection or instance overview is enabled for an instance. To modify the status of an instance, click the **Edit** icon in the **Status** column; to modify the status of multiple instances at a time, select the instances in the list and click **Custom Settings** at the top. You can filter data by status.
- **Health Score**: this column displays the instance health score (the higher the score, the healthier the instance) rated during periodic health checks. You can sort data by health score.
- **Exception Alarm**: this column displays the number of exceptions of an instance detected by "24/7 Exception Diagnosis". You can click the number in the column to view more details and sort data by the number.
- **Group**: in this column, click the **Edit** icon to select the default group or create a group for an instance. You can also select one or more instances in the list and click **Manage Group** at the top to switch them to another group or add them to a new group.

- **Operation**: in this column, click **Performance Optimization** and enter the **Performance Optimization** page to view instance performance status.
![](https://main.qcloudimg.com/raw/3d4dcfd44e68c6b4a8223eedac65aa66.png)


## Custom Settings
DBbrain provides custom settings. You can enable or disable database inspection or instance overview for an instance as needed. After database inspection or instance overview is enabled, the instance will be displayed on the database inspection page or the instance overview page.
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/monitor) and select **Instance Management** on the left sidebar. On the displayed page, select a database type at the top.
2. In the list, select one or more instances and click **Custom Settings**.

3. In the pop-up dialog box, enable or disable database inspection or instance overview. Click **View Details** to view basic information (instance ID/name and configurations) of the selected instance.


