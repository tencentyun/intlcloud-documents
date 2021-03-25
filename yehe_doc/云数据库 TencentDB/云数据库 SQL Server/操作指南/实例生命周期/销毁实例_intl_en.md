## Operation Scenarios
Based on your business needs, you can return pay-as-you-go instances in the console in a self-service manner.
- After a pay-as-you-go instance is returned, it will be moved to the TencentDB recycle bin and retained there for 24 hours. During the retention period, the instance cannot be accessed but can be restored.

After an instance is returned, once its status changes to "Isolated", no fees related to it will be incurred.
>!
>- After the instance is terminated, its data cannot be recovered, and its backup files will be terminated too, so the data cannot be restored in the cloud. Please store your backup files safely elsewhere in advance.
>- When the instance is terminated, its IP resources will be released simultaneously. If the instance has read-only instances or pub/sub configuration:
>  - Read-only instances will be terminated at the same time.
>  - After the instance is terminated, the existing pub/sub configuration on the instance will be deleted.


## Directions
1. Log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver), select the target instance in the instance list, and select **More** > **Terminate/Return** in the "Operation" column.
![](https://main.qcloudimg.com/raw/be837273695eb17b86447852317fb45f.png)
2. In the pop-up dialog box, indicate your consent and click **Terminate**.
![](https://main.qcloudimg.com/raw/eed621d2fb6827d94ab5b2875a42fc84.png)


