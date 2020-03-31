## Operation Scenario
Instance restart is a common maintenance method for TencentDB for MariaDB and is similar to restarting a local database. This document describes how to restart an instance in the console.

## Precautions
- **Preparation for restart:** during the restart, the instance cannot provide services. Therefore, before the restart, please ensure that TencentDB for MariaDB has stopped accepting business requests. During the restart, dirty pages will be generated if the business write volume is high. In this case, the restart may fail in order to shorten the business interruption.
- **Restart method:** you are recommended to restart an instance by following the steps provided by Tencent Cloud instead of running the restart command on the instance.
- **Restart period:** generally, it takes only a few minutes to restart an instance.
- **Physical instance features**: restarting an instance does not change its physical features or private IP.


## Directions
1. Log in to the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql).
2. In the instance list, select one or more instances to be restarted and click **Restart** above.
![](https://main.qcloudimg.com/raw/1dff721fa100af69d3815a9eed73e806.png)
3. In the pop-up dialog box, select the restart rule and click **OK** to restart a single instance or multiple instances in batches.
