## Isolating Instance
Once isolated, an instance cannot be used or accessed; however, it is not terminated or deleted. You can recover it in the console. After isolation, resource capacity will not be released, and the most basic data replicas will be retained. After the isolation period elapses, the instance will be completely terminated.
- A pay-as-you-go instance can be returned manually in the [console](https://console.cloud.tencent.com/dcdb). After the instance is returned, it will be in "isolated" status and retained for 24 hours, during which it cannot be accessed. If you want to restore it, you can do so in the instance list.

After an instance is returned, once its status changes to "isolated", no fees related to it will be incurred.

>!
>- After an instance is isolated, its IP will be released, and you may not get back the original IP after the instance is recovered.
>- After an instance is isolated, you cannot upgrade it, modify its parameters, create or modify an account for it, roll it back, add sets to it, or rename it.
>

### Directions
1. Log in to the [TDSQL for MySQL Console](https://console.cloud.tencent.com/dcdb), select an instance and click **More** > **Terminate/Return** above the instance list.
2. In the pop-up dialog box, indicate your consent and click **OK**
![](https://main.qcloudimg.com/raw/16f8187856e09385505c70bde7fb3912.png)
3. Return to the instance list. The status of the instance has changed to **isolated**, and you can choose to **restore/start up** the instance.

## Recovering Instance
Instance recovery is to recover an isolated instance to its normal running status. The recovery may take several minutes to complete. In addition, the recovered instance may have a new IP rather than the original IP before isolation.

## Terminating Instance
If you do not need an instance any longer, you can return it, and it will be isolated. An isolated instance will be completely terminated after expiration.

### Notes
- After an instance is terminated completely, its data will not be recoverable. Please back up the data in advance.
- When the instance is terminated, its IP resources will be released simultaneously. If it has a disaster recovery instance, the disaster recovery instance will stop the sync connection and automatically promote to master instance.



