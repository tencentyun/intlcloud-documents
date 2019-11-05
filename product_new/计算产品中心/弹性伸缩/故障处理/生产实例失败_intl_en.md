## Problem Description
Scaling activities may fail due to many reasons. If this happens, timely troubleshooting can ensure proper execution of scaling activities.
<!--
View the status of scaling groups in the [Scaling group](https://console.cloud.tencent.com/autoscaling/group). If <img style="margin:-3px 0;" src="https://main.qcloudimg.com/raw/df9771a6e2211e3f418ce257051313c3.png"> is displayed, the latest scaling activity of the scaling group has failed, see the figure below:
>Mouse-over the icon to view the cause.
>
![](https://main.qcloudimg.com/raw/8872d47c9f5966e23db7574c069ca124.png)
-->
## Problem Analysis
### Viewing the Cause
Perform the following steps to view details about the failure:
1. Click the ID of a failed scaling group in the [Scaling group](https://console.cloud.tencent.com/autoscaling/group).
2. Select **Scaling Activity** to view details, see the figure below:
![](https://main.qcloudimg.com/raw/f6a022c51ec8ed3931efd5b7d3902aad.png)

### Troubleshooting According to the Reasons
Troubleshoot the problems based on the cause of failure as instructed below. Common causes of scaling activity failures are as follows:


### Causes of Scaling Activity Failures
The causes are classified into the following types:
 - [CVM issues](#cvm)
 - [Image issues](#mirror)
 - [Network issues](#net)
 - [CBS issues](#cbs)
 - [CLB issues](#load)
 - [Others](#other)
 

 


## Troubleshooting

<span id="cvm"></span>
### CVM Issues
#### CvmSoldOut
Cause: The specified resource inventory is insufficient.
Solution: Configure Multi-model in the launch configuration, and select other instance specifications and AZs.

#### InvalidInstanceType
Cause: The specified instance specification is not available.
Solution: Select an available instance specification in the launch configuration. For more information, see [Instance Specifications](https://intl.cloud.tencent.com/document/product/213/11518).

#### InvalidDiskConfig
Cause: The current system disk does not support the model.
Solution: Check the scaling configuration and modify the system disk type. It is recommended to select premium cloud disks or SSD disks.

#### QuotiesQuotaNotEnough
Cause: A CVM purchase quota is assigned to each user. For the default quota of pay-as-you-go CVM instances, see [Purchase Limits for Pay-as-You-Go CVM Instances](https://intl.cloud.tencent.com/document/product/213/2664).
AS will not be able to provide CVMs if this quota is exceeded.
Solution: Reduce the number of scale-out CVMs or apply to raise the quota by [Submitting a Ticket](https://intl.cloud.tencent.com/document/product/213/2664).

####  InstanceTypeNotFound
Cause: The model defined in the launch configuration is incorrect or not available.
Solution: Change the launch configuration.

<span id="mirror"></span>
### Image Issues
#### ImageNotFound
Cause: The image does not exist or has become invalid.
Solution: Check the corresponding configuration in the launch configuration.

#### ImageTooLarge
Cause: The system disk capacity is smaller than the image size.
Solution: Check the launch configuration and increase the system disk capacity or use a smaller image.

<sapn id="net"></span>
### Network-related
#### DpdkVpcOnly
Cause: The selected model type only supports VPC.
Solution: Do not use the model on the basic network. Deselect the model in the launch configuration.

#### SubnetIPNotEnough
Cause: The number of IPs on the VPC subnet is limited.
Solution: Create a subnet and increase its CIDR.


<sapn id="cbs"></span>
### CBS Issues
#### DiskSoldOut
Cause: The specified resource inventory is insufficient.
Solution: Enable the default CBS function in the launch configuration.



#### InvalidDiskConfig
Cause: The current system disk does not support the model instance.
Solution: Check the scaling configuration and modify the system disk type. You are advised to select a high-performance CBS or SSD.

<sapn id="load"></span>
### CLB Issues
#### LbNotFound
Cause: CLB does not exist or has become invalid. 
Solution: Check the corresponding configuration in CLB and ensure that the CLB instance associated with the scaling group works properly.


#### LbListenerNotFound
Cause: The listener in CLB does not exist or has become invalid. 
Solution: Check the corresponding configuration in CLB and ensure that the CLB instance associated with the scaling group works properly.

#### LbLocationNotFound
Cause: The forwarding domain name or URL of the listener in CLB does not exist or has become invalid. 
Solution: Check the corresponding configuration in CLB and ensure that the CLB instance associated with the scaling group works properly.

#### LbNotReady
Cause: A CLB job is ongoing.
Solution: Reduce manual operations for a scaling group during a scaling activity to avoid operation exclusions.

<sapn id="other"></span>
### Others
#### LifecycleHookActionAbandon
Cause: A lifecycle hook for scale-out is configured for the scaling group. It is triggered during scale-out of the scaling group and is finally rejected. As a result, the scaling activity is rolled back, and the scale-out instance is released.
Solution: Check the execution policy of the lifecycle hook.
