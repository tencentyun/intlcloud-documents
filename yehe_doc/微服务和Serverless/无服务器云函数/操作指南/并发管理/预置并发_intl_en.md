Provisioned concurrency can start concurrent instances in advance according to the configuration. SCF will not repossess these instances; instead, it will ensure as much as possible that a corresponding number of concurrent instances are available to process requests.

You can use this feature to set the quota of provisioned concurrent instances for a specified function version, so as to prepare computing resources in advance and reduce the duration for cold start and initialization of runtime environment and business code.

>?The provisioned concurrency feature will be officially launched on November 1, 2021, with the following adjustments and new capabilities:
>- Idle provisioned concurrency fees will be charged for the instances that have been configured and started but are not in use. If you don't need to use provisioned concurrency, please be sure to disable it so as to avoid unnecessary fees.
>- Scheduled provisioned concurrency scaling is provided to increase/decrease the provisioned concurrency automatically, which helps reduce the idle fees.
>- The concurrency calculator and capabilities to view the monitoring data of concurrent instances on each version are added, so you can further understand your business details and set the provisioned concurrency according to your business conditions.


## Overview

Provisioned concurrency addresses the problem of concurrent instance initialization when requests are received at the version level. After you configure provisioned concurrency for a function version, the following effects will be achieved:

1. SCF will **immediately start concurrent instances** until the configured value is reached.
2. SCF will **not repossess provisioned concurrent instances**, and it will guarantee a number of provisioned concurrent instances as much as possible.

The speed of starting provisioned concurrency is separate from the speed of starting elastically invoked concurrent instances, and starting provisioned concurrency will not occupy the speed of starting 500 concurrent instances per minute at the region level. SCF will adjust the speed of starting provisioned concurrency based on your business, which is 100 concurrent instances per minute by default.

SCF will not repossess provisioned concurrent instances, but concurrent instances may become unavailable due to exiting the process or exceeding the memory limit. Once any instances become unavailable, SCF will repossess them and prepare new concurrent instances to maintain the configuration of provisioned concurrent instances. During this period, the number of actual concurrent instances may be temporarily smaller than the number of provisioned concurrent instances, and fees will not be charged for concurrent instances that are not started. You can view the start status of provisioned concurrency in **number of concurrent executions and provisioned concurrency** in the function monitoring data.

Provisioned concurrency **can be configured only on published versions but not the `$LATEST` version**. The `$LATEST` version is in an editable state, but provisioned concurrency needs to start concurrent instances before requests are received. To ensure the business stability and avoid version inconsistency caused by code and configuration editing, provisioned concurrency can be configured only on published versions. The code and configurations of published versions cannot be changed, so they are suitable for the production environment. For more information, see [Version Management](https://intl.cloud.tencent.com/document/product/583/35953).


## Provisioned Concurrency and Concurrency Management

Provisioned concurrency can help you solve the problem of long initialization of functions, so that they can respond to requests more quickly. It should be noted that provisioned concurrency is not a capability of the concurrency management system, and setting provisioned concurrency will not affect the maximum number of concurrent requests a function can process, which depends entirely on the function's reserved quota or region-level concurrency quota.

Take a function version with a configured memory of 128 MB as an example:

| Business Scenario | Average Business Concurrency | Provisioned Concurrency              | Function Reserved Quota          | Effect                                                         |
| :----------: | ------------ | -------------------- | -------------------- | ------------------------------------------------------------ |
|   Default condition  | 100 concurrent instances      | Not configured               | Not configured               | All concurrent instances need to be initialized when they process requests for the first time. The concurrency quota of the function is affected by other functions under the same account and may be exceeded. |
|   Function disablement   | 100 concurrent instances      | Not configured               | 0 MB (0 concurrent instances)         | The reserved quota is 0, the function is disabled, and all requests will get an overrun error.              |
| No provisioned concurrency required | 100 concurrent instances     | Not configured               | 19,200 MB (150 concurrent instances) | All concurrent instances need to be initialized when they process requests for the first time. 150 concurrent instances can be guaranteed, and an overrun error will occur if this limit is exceeded. |
|   80% provisioning   | 100 concurrent instances      | 10,240 MB (80 concurrent instances) | 19,200 MB (150 concurrent instances) | 80 concurrent instances don't need to be initialized, and 20 concurrent instances need to be initialized when they are invoked for the first time. 150 concurrent instances can be guaranteed, and an overrun error will occur if this limit is exceeded. |
|   100% provisioning   | 100 concurrent instances      | 12,800 MB (100 concurrent instances) | 19,200 MB (150 concurrent instances) | 100 concurrent instances don't need to be initialized, and excessive concurrent instances need to be initialized when they are invoked for the first time. 150 concurrent instances can be guaranteed, and an overrun error will occur if this limit is exceeded. |
|   Full provisioning   | 100 concurrent instances      | 19,200 MB (150 concurrent instances) | 19,200 MB (150 concurrent instances) | All concurrent instances don't need to be initialized. 150 concurrent instances can be guaranteed, and an overrun error will occur if this limit is exceeded. |
|   Overprovisioning   | 100 concurrent instances       | 25,600 MB (200 concurrent instances)  | 19,200 MB (150 concurrent instances) | It is the same as full provisioning except that it incurs additional fees for 50 more provisioned concurrent instances.           |


The concurrency management system (region-level concurrency quota and function-level reserved quota) is responsible for processing requests concurrently, while provisioned concurrency is responsible for ensuring that there are concurrent instances available to process requests. The decoupling of the two can implement capabilities such as [traffic switch with no initialization process](#grayscale).


## Provisioned Concurrency Limits

The configured provisioned concurrency quota is subject to the account-level quota; in other words, **the total provisioned concurrency quotas of all versions of all functions in a region is less than or equal to the concurrency quota at the account level**.





## Directions

### Adding provisioned concurrency

For a published function version, you can set a desired number of provisioned concurrent instances.

>! Provisioned concurrency can be set for a function version only after the [version is published](https://intl.cloud.tencent.com/document/product/583/15371).

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the **Function Service** list page, select the name of the target function to enter the **Function Management** page.
3. On the **Function Management** page, select **Concurrency Quota** on the left sidebar to enter the **Concurrency Quota** page.
4. On the **Concurrency Quota** page, select **Provisioned Concurrency** on the right to enter the **Provisioned Concurrency** page.
5. On the **Provisioned Concurrency** page, click **Add Provisioned Concurrency** as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/24aae04ac9ec1f9fb67131b48d40f9ab.png)
6. In the **Add Function Provisioned Concurrency** window that pops up, select the desired version and the number of provisioned concurrent instances and click **Submit** as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/a7cfbb86526b0d6185c5c379219af68f.png)
   After completing the settings, you can view the configuration status in **Provisioned Concurrency**. It will take some time for the SCF backend to add the instances and display the number of ready-to-start concurrent instances and completion status in the list.

### Updating provisioned concurrency

After the SCF backend adds the provisioned concurrent instances, you can modify the number of concurrent instances as needed.

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the **Function Service** list page, select the function for which to update the provisioned concurrency to enter the **Function Management** page.
3. On the **Function Management** page, select **Concurrency Quota** on the left sidebar to enter the **Concurrency Quota** page.
4. On the **Concurrency Quota** page, select **Provisioned Concurrency** on the right to enter the **Provisioned Concurrency** page.
5. On the **Provisioned Concurrency** page, select **Set** on the right of the target version as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/7653ff90ffd7035608e6a97d340ac80d.png)
6. In the **Set Function Provisioned Concurrency** window that pops up, update the set value and click **Submit**.
   After the settings are completed, the SCF platform will adjust the number of concurrent instances according to your modification in a certain period of time.


### Deleting provisioned concurrency

If you no longer use a provisioned concurrency configuration, you can delete it.

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the **Function Service** list page, select the function for which to delete the provisioned concurrency to enter the **Function Management** page.
3. On the **Function Management** page, select **Concurrency Quota** on the left sidebar to enter the **Concurrency Quota** page.
4. On the **Concurrency Quota** page, select **Provisioned Concurrency** on the right to enter the **Provisioned Concurrency** page.
5. On the **Provisioned Concurrency** page, select **Delete** on the right of the target version as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/932ddece7c6d9303b5852ac064db09e6.png)
6. In the **Delete Function Provisioned Concurrency Quota** window that pops up, click **OK**.
   After the configuration is deleted, the SCF backend will gradually repossess concurrent instances.

## Operations

### [Using provisioned concurrency for traffic switch](id:grayscale)

You can set the reserved quota for a function based on the volume of concurrent business requests and configure provisioned concurrency based on the traffic switch needs as instructed below:

1. Publish a new version.
2. Set the desired provisioned value for the new version.
3. Wait for the provisioned concurrent instances of the new version to be started completely.
4. Gradually switch the traffic from the previous version to the new version through [traffic routing configuration](https://intl.cloud.tencent.com/document/product/583/35952). If a problem occurs, switch the traffic back to the previous version.
5. Switch the traffic completely to the new version and delete the provisioned concurrency of the old version if nothing goes wrong after a period of time.

Taking the scenario listed in the following table as an example, when a function has a reserved quota of 150 concurrent instances (the function can concurrently process up to 150 requests), you can set 100 provisioned concurrent instances for multiple versions (100 instances are started for each version), so as to switch the traffic with no initialization needed.

| Business Scenario | Average Business Concurrency | Provisioned Concurrency              | Function Reserved Quota          | Effect                                                         |
| :------: | ------------ | --------------------- | --------------------- | ------------------------------------------------------------ |
|   100% provisioning   | 100 concurrent instances      | 12,800 MB (100 concurrent instances) | 19,200 MB (150 concurrent instances) | 100 concurrent instances don't need to be initialized, and excessive concurrent instances need to be initialized when they are invoked for the first time. 150 concurrent instances can be guaranteed, and an overrun error will occur if this limit is exceeded. |

As shown in the figure below, 100 provisioned concurrent instances is configured for both version 4 and version 5, and you can use the traffic grayscale capability to switch the 100 concurrent instances of the business from version 4 to version 5. No matter how the 100 concurrent instances are allocated to versions 4 and 5 according to any proportion, no instances will need to be initialized, thus making it easier for you to publish a version and switch traffic more quickly.


![](https://qcloudimg.tencent-cloud.cn/raw/6031d3d45489466e980f9a3ae91fc216.png)
