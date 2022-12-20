## Overview
Role management provides Ops and operation features at the service role level. You can restart, pause, and maintain service roles at the node level. Role status can be monitored to help you stay on top of the real-time status of role processes.

### Glossary
- Restart: The nodes under the selected service role will be restarted on a rolling basis.
- Pause: The nodes under the selected service role will be paused. They can be resumed by using the **Start** feature.
- Maintenance: The process daemon will be stopped on the nodes under the selected service role, so when a process becomes abnormal for various reasons, no alarm or automatic recovery will occur. This is suitable for node debugging. You can use the **Exit Maintenance** feature to resume the daemon.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Service** and click **Operation** > **Role Management** in the top-right corner of the target component block. The following uses HDFS as an example.
3. The **Role Management** list displays the current service role's health status, operation status, configuration group, node type, maintenance status, server IP, and last restarted time. You can select a role and **restart, maintain, start, or pause** it.
>? The **Health Status** column displays the running status of the current role. The **Operation Status** column displays user operations. The **Maintenance Status** column displays whether the role is under maintenance.

![](https://main.qcloudimg.com/raw/d5547ec27b700d122523239f8ebba676.png)
## Health Status
| Health Status | Description |
|---------|---------|
| Good | Port check is responded to within 5s. |
| Risky | Port check is responded to within 5s–10s. |
| Unavailable | Port check is not responded to within 10s. |
| Not checked | Roles in the maintenance mode or in Stopped operation status are not checked. |
| Unknown | The checker is abnormal or down. |
