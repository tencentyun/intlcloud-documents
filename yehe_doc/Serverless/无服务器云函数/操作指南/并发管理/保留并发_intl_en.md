The reserved concurrency quota is the maximum quota used to guarantee the available concurrency of a function. By configuring the reserved concurrency quota, the function can start enough concurrent instances within the quota, and the maximum number of concurrent instances can reach the configured quota. After the reserved concurrency quota is set, the function no longer shares the concurrency quota at the account level with other functions, which can reduce the possibility of concurrency overrun and guarantee smooth function execution.



## Reserved Concurrency Quota Configuration Description

- The reserved concurrency is configured on the function according to the memory quota. After configuration, the sum of the memory configured for the specific running instances of the function cannot exceed the configured quota.
- If the function has the reserved concurrency quota set, then the sum of all provisioned concurrency quotas for all versions of the function cannot exceed the reserved concurrency quota.
- The configured reserved concurrency quota will be deducted from the remaining configurable quota at the account level, reducing the shared account quota.
- The quota at the account level will reserve 12,800 MB, which cannot be configured as reserved or provisioned concurrency quota and will be used to run functions that don't have such quotas set.
- Setting the function reserved concurrency quota to 0 can stop the running of the current function. All requests for the function will return a concurrency overrun error.



## Reserved Concurrency Operations

### Setting reserved concurrency

You can set the desired reserved concurrency quota for a function in the following steps:
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. On the **Function Service** list page, select the name of the target function to enter the **Function Management** page.
3. On the **Function Management** page, select **Concurrency Quota** on the left sidebar to enter the **Concurrency Quota** page.
4. On the **Concurrency Quota** page, click **Set** on the right of **Reserved Quota**.
5. In the **Set Function Reserved Concurrency Quota** window that pops up, set the desired reserved concurrency quota and click **Submit** as shown below:
![](https://main.qcloudimg.com/raw/257598e0b96f29194a37ca7ea40bc3b6.png)
Then, you can view the configuration status in the **Reserved Quota** section on the **Concurrency Management** page.

### Deleting reserved concurrency

If you no longer use reserved concurrency, you can delete it. After the deletion, the function will share the concurrency quota at the account level with other functions.

>? Deleting reserved concurrency is different from setting reserved concurrency to 0. Setting the reserved concurrency to 0 will cause the function to have no available quota for running and thus stop the function from processing the triggering event.

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. On the **Function Service** list page, select the name of the target function to enter the **Function Management** page.
3. On the **Function Management** page, select **Concurrency Quota** on the left sidebar to enter the **Concurrency Quota** page.
4. On the **Concurrency Quota** page, click **Delete** on the right of **Reserved Quota**.
5. In the **Delete Function Reserved Quota** window that pops up, click **OK** as shown below:
![](https://main.qcloudimg.com/raw/aed1c7174783fb147ebaa6efde705acb.png)
   After the configuration is deleted, the SCF backend will gradually repossess concurrent instances.
