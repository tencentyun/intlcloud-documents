## Isolating Instances
An instance can be isolated when you no longer use it. Once isolated, the instance can neither be used nor accessed (but is not eliminated yet), and will be moved to the recycle bin, where you can restore or eliminate it or it will be automatically eliminated when it expires. Even though the instance is isolated, the space occupied by its resources is not freed, and it still has the most basic data replicas.

- You can log in to the [console](https://console.cloud.tencent.com/mariadb/instance/index), select the pay-as-you-go instance in the instance list, click **Terminate/Return** to return it manually. After the instance is returned, it is in the **Isolated* status and will be retained for 24 hours, during which it cannot be accessed. To restore it, you can do so in the recycle bin list.

After an instance is returned, once its status changes to "isolated", no fees related to it will be incurred.

>!
>- After an instance is isolated, its IP will be released, and you may not get back the original IP after the instance is restored.
>- After an instance is isolated, you cannot upgrade it, modify its parameters, create or modify an account for it, roll it back, or rename it.

### Directions
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld). In the instance list, select an instance, and click **More** > **Terminate/Return** at the top.
2. In the pop-up dialog box, indicate your consent and click **OK**.
![](https://main.qcloudimg.com/raw/16f8187856e09385505c70bde7fb3912.png)
Go to the recycle bin where the instance is in the "isolated" status.

## Restoring Instances
An isolated instance can be restored to its normal running status, which may take several minutes. The restored instance may have a new IP rather than the original IP before isolation.

### Directions
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld), locate the instance in the recycle bin list, and click **Restore/Start up**.
2. In the pop-up dialog box, click **OK**.

## Terminating Instances
If you don't need an instance anymore, you can return it. Once returned, it is in the "isolated" status and moved to the recycle bin, where it will be automatically eliminated when it expires, or you can click **Eliminate Now** to completely terminate it.

### Notes
- After an instance is eliminated, its data will not be recoverable. Please back up the data in advance.
- After an instance is eliminated, its IP resources will be released simultaneously, and its disaster recovery instance will stop the sync connection and automatically promote to primary instance.
