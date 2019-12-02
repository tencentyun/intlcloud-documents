## Operation Scenarios
TencentDB for Redis supports read/write separation for business scenarios with more reads but less writes, which can well cope with read requests concentrating on frequently read data. It supports up to 1-master 5-slave mode to offer 5x read performance.

>After read/write separation is enabled, certain fees will be charged for the read-only replicas. For more information, please see [Pricing](https://intl.cloud.tencent.com/document/product/239/9894).

## Directions
1. Log in to the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis).
2. On the instance list page, click the name of the TencentDB instance for which you want to create a read-only instance to enter the instance details page.
3. On the **Manage Node** page, click **Read-only Replica** to enable read/write separation.
![](https://main.qcloudimg.com/raw/31acc5f160e4b4160f9b79a890990200.png)

