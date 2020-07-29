## Feature Overview
Role management provides OPS and operation features at the role service level. You can restart, pause, and maintain cluster service roles. Role status can be monitored to help you stay on top of the real-time status of role processes.

### Glossary
- Restart: the selected service role will be restarted on a rolling basis by server.
- Pause: the servers in the selected service role will be paused, which can then be resumed by using the **Start** feature.
- Maintenance: the process daemon will be stopped for the servers in the selected service role. When a process becomes exceptional for various reasons, no alarming or automatic recovery will occur. This is suitable for server debugging. You can use the **Exit Maintenance** feature to resume the daemon.


## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select the target cluster in **Cluster List**, and click **Details** to enter the cluster details page.
2. On the cluster details page, select **Cluster Service** and click **Operation** > **Role Management** in the top-right corner of the target component block. The following uses Hive as an example.
3. The **Role Management** column displays whether the current service is **running** or **paused**, and the **Maintenance Status** column displays whether the current service is under maintenance.
![](https://main.qcloudimg.com/raw/d5547ec27b700d122523239f8ebba676.png)
