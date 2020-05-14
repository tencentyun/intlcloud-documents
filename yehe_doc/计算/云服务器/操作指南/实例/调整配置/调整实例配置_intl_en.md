## Scenario

Hardware devices of Tencent Cloud CVM instances can be adjusted quickly and conveniently. This document describes the methods and precautions for configuration upgrade, downgrade, and cross-model adjustment.

## Prerequisites

You can adjust an instance's configuration when the instance is either started or shut down.
> 
> - When the instance is **shut down**, you can directly adjust its configuration in the console.
> - When the instance is **started**, you can adjust the configuration online and confirm the forced shutdown of the instance. The adjusted configuration takes effect after the instance is restarted.
> - You can adjust configurations **in batches** online for multiple instances. If an instance in the batch of instances is **started**, you need to confirm forced shutdown for the instance. The adjusted configuration takes effects after the instance is restarted.

## Limits and Impacts

### Configuration adjustment limits

Only the configurations of instances **whose system and data disks are both CBS cloud disks** can be adjusted.
- Upgrading the configuration:
The number of configuration upgrades is not limited. The upgraded configuration takes effect immediately.
- Downgrading the configuration:
 The configurations of pay-as-you-go instances can be downgraded at any time an unlimited number of times.
- Adjustment across instance families: configurations can be adjusted between different instance families without the need of data migration.
During configuration adjustment, target instance types depend on the instance types provided in the current availability zone. Pay attention to the following limits:
 - **Spot instances** do not support cross-model configuration adjustment.
 - **Exclusive instances** do not support cross-model configuration adjustment. The configuration adjustment scope is limited to the remaining resources of the dedicated host where the instance is located.
 - **Heterogeneous instances, such as GPU and FPGA instances,** cannot be used as the source or destination instance type for configuration adjustment across instance families.
 - **Instances configured with a basic network** cannot be adjusted to instances that only support VPC instances.
 - If the target instance type does not support the CBS type configured for the current instance type, the configuration cannot be adjusted.
 - If the target instance type does not support the image type configured for the current instance type, the configuration cannot be adjusted.
 - If the target instance type does not support the ENI or ENI quantity configured for the current instance type, the configuration cannot be adjusted. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/576/18527).
 - If the target instance type does not support the public network bandwidth upper limit configured for the current instance type, the configuration cannot be adjusted. For more information, see the [Public Network Bandwidth Cap](https://intl.cloud.tencent.com/document/product/213/12523).

### Impacts

The private IP address of an instance may be changed after configuration adjustment. If the private IP address of an instance is changed after configuration adjustment, a prompt appears on the configuration adjustment page. If no prompt appears, the private IP address is not changed.

## Directions

>
> - If your business changes, you can adjust configurations.
> - During configuration upgrade, upgrade the configuration and pay any fees involved.
> - During configuration downgrade, confirm the refund details and forcibly shut down and restart your CVM instance for the new configuration to take effect. Then, the CVM instance runs based on the new configuration.

### Configuration adjustment in the console

#### Adjusting the configuration of a single instance

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm) and click **Instances** to view the CVM instance list.
2. Locate the target instance and choose **More** > **Resource Adjustment** > **Adjust Configuration** in the **Action** column on the right, as shown in the following figure:
![](https://main.qcloudimg.com/raw/65541031befe2d0144227cf5a616e161.png)
3. In the "Select target configuration" step, confirm the instance status and operation, **select the required model and instance type, confirm the type and performance parameters**, and click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/818fbf0dfa791ad5d5a76186eefba019.png)
4. Based on the instance billing method, confirm the fees and click **Next**.
	- Pay-as-you-go instances: confirm the amount to be frozen for the new instance type. After the configuration is adjusted, pay-as-you-go instances are charged starting from the tier-1 price. Confirm the billing rules before configuration adjustment, as shown in the following figure:
	![](https://main.qcloudimg.com/raw/25f8630836acdfe274357142d8609c5d.png)
5. In the "Shutdown CVM" step, carefully read the prompt for different instance running states.
 - If the current instance is running, carefully read the prompt and select "Agree to a forced shutdown", as shown in the following figure:
![](https://main.qcloudimg.com/raw/e016f2cc674938acd0046115f007669b.png)
 - If the current instance is shut down, the following prompt appears:
![](https://main.qcloudimg.com/raw/8385495393237523d0d71460a7b7009b.png)
6. Click **Adjust Now** to go to the order page and pay for the order. 

### Configuration adjustment through APIs 

You can use the ResetInstancesType API to adjust the instance configuration. For more information, see the [ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239) API document.





