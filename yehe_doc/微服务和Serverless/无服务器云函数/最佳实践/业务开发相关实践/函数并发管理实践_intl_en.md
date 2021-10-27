## Scenarios


SCF now provides concurrency quota management capabilities at three levels. With this feature, you can get greater permissions to control function concurrency to adjust the concurrency quickly based on your business needs instead of applying for concurrency quota.


>? [Function concurrency](https://intl.cloud.tencent.com/document/product/583/37040) management feature has been launched. You can configure the [reserved quota](https://intl.cloud.tencent.com/document/product/583/39464) for a function. And the [provisioned concurrency](https://intl.cloud.tencent.com/document/product/583/37704) feature is in beta test phase.




The default function concurrency limit is set to 300 by default. For infrequent businesses with low function usage, the 300 concurrent instances were generally sufficient. However, in cases where high concurrency was required, such as business surges and large-scale campaigns, you needed to submit a ticket to apply for an increase in the concurrency quota. This scheme has the following three challenges:

- Every time your business surged, you needed to contact Tencent Cloud to apply for an increase in the function quota, which was time-consuming. 
- Your business growth might be restricted during the application processing time.
- The application might be rejected due to insufficient business scale during the evaluation, leading to reapplication and making the process inefficient.

This document describes the concurrency management feature in detail and provides configuration suggestions for a variety of use cases.



## Features

### Concurrency capabilities

SCF provides the following concurrency management options:

- Customize the concurrency quota for individual functions
- The concurrency quota is now configure at the account level, instead of the function level.
- Each account is allocated with a concurrency quota, which is shared by all functions under it. You don’t need to separately apply for a quota for high-concurrency functions.

Each account is allocated with a concurrency quota of 128,000 MB, which allows 1,000 function instances with the 128 MB specification to run concurrently. You don’t need to apply for a quota increase to sustain your business growth. See below for the trend of concurrency usage:
![](https://main.qcloudimg.com/raw/ec9931cf41c7ce47251b2dbaadb170f5.png)


### Relationship between memory and concurrency quota

Concurrency quota is calculated by the memory. A function with a higher memory configuration occupies a larger share of the quota during concurrent execution, while a function with a smaller memory configuration memory occupies a smaller share of the quota during concurrent execution.

Since the resource usage billing item of the SCF service is highly related to the configured memory of functions, if you need to control the quota through the memory configuration, we recommend you select an appropriate function memory value for your business, which can effectively control the overall costs. The memory changes are as shown below:
![](https://main.qcloudimg.com/raw/3498140e74bbab6b328d9122bbc8ea86.png)





## Practice

### Concurrency use cases

If multiple businesses under your account use SCF for support at the same time, you should schedule the concurrency quotas of functions as needed and make reasonable settings according to different business characteristics. The following analyzes the types, characteristics, and requirements of different businesses:

| Business Type | Characteristics | Requirements |
|---------|---------|---------|
| Frontend business | There are peak hours and off-peak hours | Requires a fast page load speed and allows  a certain fault tolerance is allowed |
| Data processing business | The operation is stable with little fluctuation | Delays, fluctuations, and failures are unacceptable |
| OPS tasks | Tasks are scheduled and occasional | There is no need to pay much attention as long as the tasks run normally |
| Video processing business | The amount of concurrency is not large, but the computation is complicated and time-consuming | On-demand scheduling is acceptable as long as tasks can automatically run again upon failure |


According to different business characteristics, fault tolerance limits, business fluctuations, and delay requirements, different configurations can be made for different use cases as recommended below:

[](id:proposal)
<dx-tabs>
::: Frontend business
Frontend businesses require a fast page load speed and have peak hours and off-peak hours. You can configure the provisioned concurrency quota (e.g. 60% of the maximum usage), and leave out the reserved concurrency quota, so that the total quota can be fully utilized during peak hours. See below for the trend of concurrency usage:
![](https://main.qcloudimg.com/raw/873e43f714412798dfd301dcce8ef908.png)
:::
::: Data processing business
Data processing businesses with little fluctuation but low fault tolerance, you can configure the reserved concurrency quota for the function, so that the quota is not shared by other businesses. See below for the trend of concurrency usage:
![](https://main.qcloudimg.com/raw/68d8e72e923aa4a81682160124398fbf.png)
:::
::: OPS task
For OPS tasks that are not demanding and run regularly, you don't need to make any configurations; instead, you can simply use the account-level quota logic.
:::
::: Video processing business
For video processing businesses that have a large amount of computation where tasks are queued up for on-demand processing, a certain reserved concurrency quota can be configured for functions, so that the businesses can run at the full concurrency quota and make the most of computing resources. See below for the trend of concurrency usage:
![](https://main.qcloudimg.com/raw/1328e16954a4eeff496665a44504aa21.png)
:::
</dx-tabs>



### Reserved quota use case

The account-level quota is shared by multiple functions under the account. If multiple functions run simultaneously, functions whose concurrency is increased due to traffic/business surges may conflict with stable functions after they use up all the available quota.

**针对上述场景，有以下两种解决方案：**


In this case, you can configure reserved concurrency quota. The execution stability of specific functions can be guaranteed by assigning a certain part of the quota to them.
Note that you can also solve the issue by [submitting a ticket](https://console.cloud.tencent.com/workorder/category) to apply for a higher account-level concurrency quota.

#### Configuring reserved quota

本文以解决方案1（最大独占配额配置）为例详细介绍如何使用最大独占配额：

**Scenario**: Function A and Function B are under the same account. Function A is used for flash sale H5 pages, and Function B is used for streamline data processing on the backend. Function B launches 300 concurrent instances first for normal business running, and Function A takes the rest 700 concurrency for promotion events. In this case, if a request surge comes to Function B, no more instances can be started due to the quota limit. You can configure the reserved concurrency to keep the balance between these two funcitons.
![](https://main.qcloudimg.com/raw/9862ba9b8f8a665bf119c3565e335b8d.png)

**Sample configuration**: to ensure the reliability of data processing, which is handled by Function B, you can set the reserved concurrency quota to 350 for function B. Then, this quota will be assigned from the account level to function B exclusively, and function A will only be able to use 650 concurrent instances at most. Note that the concurrency of Function B cannot exceeds 350 even if there are still available resources within the  account-level quota. 
![](https://main.qcloudimg.com/raw/86f9d5c0fe010d5263de5c58df9ddd1a.png)

With the reserved quota, 
- The normal execution of a function is guaranteed, preventing losses caused by the function's inability to run due to usage of other functions that share the quota.
- The max concurrency of a function is limited.

**Suggestions**: 
- For functions in the development and testing phase, because of the small number of requests, little business pressure, and minimal concurrency, there is no need to configure the reserved concurrency quota, and it is fine to use the shared quota at the account level.
- For functions that run stably, the amount of concurrency can usually be determined within a small fluctuation range; therefore, you can configure a reserved concurrency quota with a little margin to ensure that the quota will not be affected by sharing.
- For functions used for operational activities where the concurrency may surge, you can increase the account-level quota to make full use of and support the business growth.


![](https://main.qcloudimg.com/raw/2395c23bbee3b79fbb21c5cb62ef8e3b.png)




### Notes
Currently, provisioned concurrency quota is set at the function version level, which is deducted from the concurrency quota at the account level or the reserved concurrency quota at the function level.

By configuring provisioned concurrency quota, you can start the required number of concurrent instances, complete the instance initialization, and wait for events to occur in advance. Requests for the function will not have a cold start time, and they can be run directly in the instances that have already been prepared and initialized.

For delay-sensitive businesses (such as frontend SSR page response) or businesses with a long initialization time (such as the model loading process of AI inference), configuring provisioned concurrency can ensure better business operation.

Meanwhile, as provisioned concurrency quota is not the upper limit of instance concurrency, when the business volume exceeds the maximum scale that the provisioned instances can sustain, the function will still launch more instances according to its reserved concurrency quota or account-level quota to support the business operation. The function quota changes are as shown below:
![](https://main.qcloudimg.com/raw/76e5c52d273f284673747e2c025ed303.png)


#### Other usages of reserved concurrency quota

The restriction or shutdown of a business can also be implemented by configuring the reserved concurrency quota. In case of emergencies, such as vulnerability attacks and out-of-control loop invocations, in order to avoid major losses, you can set the reserved concurrency quota to a very small value to avoid running out of control or even to 0 to stop function execution. For more information, please see [Reserved Concurrency](https://intl.cloud.tencent.com/document/product/583/39464). The configuration is as shown below:
![](https://main.qcloudimg.com/raw/6bcb722183d8fb14609bb90a23323584.png)
