## Idle Provisioned Concurrency Fees

**Idle provisioned concurrency fees = number of idle instances * configured memory size * idle duration * idle provisioned concurrency unit price**

- **Number of idle instances**: SCF counts the maximum concurrency of a version at a 10-second granularity. The number of idle instances is calculated by subtracting the maximum concurrency from the number of currently started provisioned instances. The calculation formula is as follows: number of idle instances = max(number of started provisioned instances - number of concurrent instances, 0).
- **Configured memory size**: the memory size configured for the provisioned concurrency of the function.
- **Idle duration**: the idle duration of the provisioned concurrency.
- **Idle provisioned concurrency price**: see [Pricing](https://intl.cloud.tencent.com/document/product/583/12281).

>? Idle provisioned concurrency is calculated in GBs (GB-second).

The provisioned concurrency feature only charges small idle fees for the instances that have been configured and started but are not in use, **while no additional fees are charged for the instances that have been configured and are in use**. In other words, only when the number of provisioned instances is greater than the number of concurrent instances for the current version will idle fees be incurred.

## Billing Example


The idle provisioned concurrency fees are calculated by multiplying the number of idle instances by the configured memory size. The blue shaded part in the figure below indicates the idle provisioned concurrency. For more information, please see [Billing Example](https://intl.cloud.tencent.com/document/product/583/12285).
![img](https://qcloudimg.tencent-cloud.cn/raw/b60ea672c33a04e7b1751318de10f907.png)

