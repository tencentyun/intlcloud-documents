The reserved concurrency quota is the upper limit of guaranteed concurrency for a function. This quota allows the function to start concurrent instances as many as the quota. After the reserved concurrency quota is configured, the function no longer shares the account concurrency quota with other functions, which can reduce the possibility of concurrency overrun and guarantee smooth function execution.



## Configuration Description
- The reserved concurrency is configured on the function according to the memory quota. After configuration, the sum of the memory configured for the specific running instances of the function cannot exceed the configured quota.
- The configured reserved concurrency quota will be deducted from the remaining configurable quota at the account level, taking up the account’s sharable quota.
- The account will reserve a quota of 12,800 MB for functions with no reserved concurrency configured.
- Setting the reserved concurrency quota to 0 will cause the running function to stop. All requests for the function will return a concurrency overrun error.



## Directions

### Setting reserved concurrency

You can set the desired reserved concurrency quota for a function in the following steps:
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. On the **Function Service** list page, select the name of the target function to enter the **Function Management** page.
3. On the **Function Management** page, select **Concurrency Quota** on the left sidebar to enter the **Concurrency Quota** page.
4. On the **Concurrency Quota** page, click **Set** on the right of the **Reserved Quota**.
5. In the **Set Function-level Reserved Concurrency Quota** window that pops up, set the desired reserved concurrency quota and click **Submit**, as shown below:
![](https://main.qcloudimg.com/raw/257598e0b96f29194a37ca7ea40bc3b6.png)
Then, you can view the configuration status in the **Reserved Quota** section on the **Concurrency Management** page.

### Deleting reserved concurrency

You can delete a reserved concurrency if you no longer need it. After deletion, the function will share the account concurrency quota with other functions.

>? Different from deleting reserved concurrency, setting the reserved concurrency to 0 will cause the function to have no available quota for running instances and thus stop the function from processing the trigger event.

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. On the **Function Service** list page, select the name of the target function to enter the **Function Management** page.
3. On the **Function Management** page, select **Concurrency Quota** on the left sidebar to enter the **Concurrency Quota** page.
4. On the **Concurrency Quota** page, click **Delete** on the right of the **Reserved Quota**.
5. In the **Delete Function’s Reserved Quota** window that pops up, click **Confirm** as shown below:
![](https://main.qcloudimg.com/raw/aed1c7174783fb147ebaa6efde705acb.png)

