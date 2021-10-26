The SCF platform provides concurrency management capabilities at the function granularity to allow you to flexibly control the concurrency of different functions.

## Concurrency Management System

Currently, SCF allows concurrency management at two levels: account-level concurrency quota and function-level reserved concurrency quota.

```
Account-Level concurrency quota
<<<<<<< HEAD
  |- Function-Level reserved quota
=======
|- Function-Level reserved concurrency quota
>>>>>>> 73d567d552bc9c5309ef6644008c9fa3dfa83c58
```

>? [Provisioned concurrency](https://intl.cloud.tencent.com/document/product/583/37704) is not included in the concurrency management capabilities; instead, it only serves as the ability to start instances in advance. Versions under the same function share the concurrency of the function.


## Account-Level concurrency quota

Each account has a total concurrency quota limit at the region level. The default value is 128,000 MB or 64,000 MB. For more information, please see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637). The concurrency quotas between regions are independent of each other and don't affect each other.

By default, the account-level concurrency quota is shared by all functions in the current region. This means that at any specific time point, the sum of actual concurrently running instances of all functions can reach up to the concurrency quota of the account. Requests exceeding the concurrency quota will encounter the overrun error (432 ResourceLimitReached). You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase the account-level quota.

You can use the function's [reserved quota](#reserved) to allocate the region-level concurrency to a certain function, so as to manage the concurrency of the function. In order to avoid the situation where functions with no reserved quota set cannot be invoked after the account-level quota is fully allocated, the SCF platform sets 12,800 MB of the account-level concurrency quota to be unallocable and only available for functions with no reserved quota set, as shown below:
![](https://main.qcloudimg.com/raw/ddb7c602bf6c101763b29af06989d686.png)

## [Reserved Quota](id:reserved)

Reserved quota is the concurrency management capability at the function level. When you set the reserved quota for a function, it will have the following two effects:

- **The reserved quota is the upper limit of the concurrency quota of this function.** The sum of the concurrency quotas of all versions is less than or equal to the reserved quota.
- After the concurrency quota is allocated to this function, it will be **exclusive to** this function and will no longer be provided to other functions.




The reserved quota is the upper limit of the function concurrency quota. You can use this capability to manage the function concurrency and control the costs so as to avoid out-of-control costs. At the same time, you can also disable a function by **setting its reserved quota to 0**. Then, all requests for this function will encounter the concurrency overrun error.

Setting the function reserved quota will occupy the concurrency quota at the region level. If the unoccupied quota at the region level (region-level quota - reserved quotas allocated to other functions - 12,800 MB) is insufficient, it cannot be set.


### Setting reserved quota

You can set the desired reserved quota for a function in the following steps:

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. On the **Function Service** list page, select the name of the target function to enter the **Function Management** page.
3. On the **Function Management** page, select **Concurrency Quota** on the left sidebar to enter the **Concurrency Quota** page.
4. On the **Concurrency Quota** page, select **Reserved Quota** to enter the **Reserved Quota** page.
5. On the **Reserved Quota** page, click **Set** on the right.
6. In the **Set Function Reserved Quota** window that pops up, set the desired reserved quota and click **Submit** as shown below:
   ![](https://main.qcloudimg.com/raw/257598e0b96f29194a37ca7ea40bc3b6.png)
   Then, you can view the configuration status in the **Reserved Quota** section on the **Concurrency Management** page.


### Deleting reserved quota

If you no longer use the reserved quota, you can delete it. After the deletion, the function will share the concurrency quota at the account level with other functions.

>? Deleting the reserved quota and setting the reserved quota to 0 are different configurations.
- **Deleting reserved quota**: the function does not have a dedicated quota and uses the shared quota in the region. The upper limit is subject to the usage of the shared quota.
- **Setting reserved quota to 0**: both the function's dedicated quota and concurrency upper limit are 0, so the function cannot run and stops responding to triggering events.
>
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. On the **Function Service** list page, select the name of the target function to enter the **Function Management** page.
3. On the **Function Management** page, select **Concurrency Quota** on the left sidebar to enter the **Concurrency Quota** page.
4. On the **Concurrency Quota** page, click **Reserved Quota** to enter the **Reserved Quota** page.
5. On the **Reserved Quota** page, click **Delete** on the right.
6. In the **Delete Function Reserved Quota** window that pops up, click **OK** as shown below:
   ![](https://main.qcloudimg.com/raw/aed1c7174783fb147ebaa6efde705acb.png)

