Provisioned concurrency can start concurrent instances in advance according to the configuration. SCF will not repossess these instances proactively; instead, it will ensure as much as possible that a corresponding number of concurrent instances are available to process requests.

The provisioned concurrency is version-specific. When it's set, the requested computing resources are prepared in advance to shorten the time required for cold start, and initialization of runtime environment and business code.

## Overview

Provisioned concurrency is a version-level configuration. When it’s configured for a function version, the following happen:

1. SCF **immediately launches instances** until the configured value is reached.
2. SCF **does not repossess provisioned concurrent instances proactively**. Instead, it guarantees the number of provisioned concurrent instances as much as possible.

The speed of launching instances for provisioned concurrency defaults to 100 instances per minute. This has nothing to do with the speed for launching instances for elastic invocation. It does not count toward the quota of 500 concurrent instances/minute at the region level. 

SCF does not repossess provisioned concurrent instances proactively. However, concurrent instances can become unavailable due to exiting the process or exceeding the memory limit. Once an instance becomes unavailable, it is released and a new instance is launched to meet the requirement of the provisioned concurrency configuration. During this period, the number of actual concurrent instances may be temporarily smaller than the number of provisioned concurrent instances. Concurrent instances do not incur charges when they are not launched. You can check the status of provisioned concurrency in **number of concurrent executions and provisioned concurrency** in the function monitoring data.

For the service stability and version consistency, provisioned concurrency **can be configured only on published versions, but not the `$LATEST` version**. For more information, see [Version Management](https://intl.cloud.tencent.com/document/product/583/35953).


## Provisioned Concurrency and Concurrency Management

Setting up the provisioned concurrency can speed up function initialization. However, the provisioned concurrency has nothing to do with the concurrency capability. It does not affect the maximum number of concurrent requests a function can process, which depends entirely on the function's reserved quota or region-level concurrency quota.

A function version with 128 MB memory is taken as an example below:

| Scenario | Average concurrency | Provisioned concurrency              | Function reserved quota          | Result                                                         |
| :----------: | ------------ | -------------------- | -------------------- | ------------------------------------------------------------ |
|   Default   | 100 concurrent instances      | Not configured               | Not configured               | All concurrent instances need to be initialized when they process requests for the first time. The concurrency quota of the function is affected by other functions under the same account and may be exceeded. |
|   Function disabled   | 100 concurrent instances      | Not configured               | 0 MB (0 concurrent instances)         | The reserved quota is 0, the function is disabled, and all requests will get an overrun error.              |
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

>! See [Publishing a version](https://intl.cloud.tencent.com/document/product/583/15371).

1. Log in to the SCF console and select **[Functions](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the **Functions** list page, select the name of the target function to enter the **Function management** page.
3. Select **Concurrency quota** from the left, go to the **Provisioned concurrency page and click **Add provisioned concurrency**
4. In the **Add provisioned function concurrency** window that pops up, select the target version, set the number of provisioned concurrent instances and click **Submit**.
   After completing the settings, you can view the configuration status in **Provisioned Concurrency**. 

### Updating provisioned concurrency

You can modify the number of concurrent instances as needed.

1. Log in to the SCF console and select **[Functions](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the **Functions** list page, select the name of the target function to enter the **Function management** page.
4. On the **Concurrency quota** page, select **Set** on the right of the target version.
4. In the **Configure provisioned function concurrency** window that pops up, update the value and click **Submit**.
   After the settings are completed, SCF will adjust the number of concurrent instances according to your modification in a certain period of time.


### Deleting provisioned concurrency

You can delete a provisioned concurrency configuration if you don’t need to use it. 

1. Log in to the SCF console and select **[Functions](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the **Functions** list page, select the name of the target function to enter the **Function management** page.
3. Select **Concurrency quota** from the left, go to the **Provisioned concurrency page, locate the version you want to delete and click **Delete** 
4. In the **Delete provisioned function concurrency** window that pops up, click **OK**.
   After the configuration is deleted, concurrent instances are released gradually. 

## More

### [Using provisioned concurrency for traffic switch](id:grayscale)

You can set the reserved quota for a function based on the volume of concurrent business requests and configure the provisioned concurrency based on the traffic switch needs as instructed below:

1. Publish a new version.
2. Set the desired provisioned value for the new version.
3. Wait for the provisioned concurrent instances of the new version to be started completely.
4. Gradually switch the traffic from the previous version to the new version through [traffic routing configuration](https://intl.cloud.tencent.com/document/product/583/35952). If a problem occurs, switch the traffic back to the previous version.
5. Switch the traffic completely to the new version and delete the provisioned concurrency of the old version if nothing goes wrong after a period of time.

In the example below, the reserved quota of the function is 150 concurrent instances, which means the function can concurrently process up to 150 requests. You can set 100 provisioned concurrent instances for multiple versions (100 instances are started for each version), so as to switch the traffic with no initialization needed.

| Scenario | Average Business Concurrency | Provisioned Concurrency              | Function Reserved Quota          | Effect                                                         |
| :------: | ------------ | --------------------- | --------------------- | ------------------------------------------------------------ |
|   100% provisioning   | 100 concurrent instances      | 12,800 MB (100 concurrent instances) | 19,200 MB (150 concurrent instances) | 100 concurrent instances don't need to be initialized, and excessive concurrent instances need to be initialized when they are invoked for the first time. 150 concurrent instances can be guaranteed, and an overrun error will occur if this limit is exceeded. |

As shown in the figure below, 100 provisioned concurrent instances is configured for both version 4 and version 5, and you can use the traffic grayscale capability to switch the 100 concurrent instances of the business from version 4 to version 5. No matter how the 100 concurrent instances are allocated to versions 4 and 5 according to any proportion, no instances will need to be initialized, thus making it easier for you to publish a version and switch traffic more quickly.


![](https://qcloudimg.tencent-cloud.cn/raw/6031d3d45489466e980f9a3ae91fc216.png)
