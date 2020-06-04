You can use the real-time session feature of DBbrain to view the real-time session information of the current instance. This document describes how to use the real-time session feature.

>Currently, real-time session is supported only for TencentDB for MySQL (excluding the Basic Edition).

## Performance and Connection Monitoring
Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/session), select **Diagnosis and Optimization** on the left sidebar, and select **Real-Time Session** at the top.
- The **Performance Monitoring** column displays in real time the number of running threads and the CPU utilization of the instance.
- The **Connection Monitoring** column displays in real time the maximum number of connections and the number of active connections of the instance.
![](https://main.qcloudimg.com/raw/03c23c17ff637f50f40a8b4d8e8e8dce.png)

## Running Threads
This section visually displays the `SHOW PROCESSLIST` command execution result of your database instance, and the displayed data is refreshed once every five seconds by default. You can filter data based on your needs using the following dimensions:
- Thread types: All, Query, or Not Sleep.
- Number of entries: 20, 50, or 100.
- Refresh intervals: 5 seconds, 15 seconds, or 30 seconds.
- You can choose to stop refresh or enable auto-refresh.
![](https://main.qcloudimg.com/raw/3108f1dabc290943262e71ca2be67323.png)
