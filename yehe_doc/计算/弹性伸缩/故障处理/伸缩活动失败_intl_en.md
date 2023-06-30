## Problem Description
Scaling activities may fail due to many reasons. If this happens, timely troubleshooting can ensure proper execution of scaling activities.
View the status of the target scaling groups in the [scaling group list](https://console.cloud.tencent.com/autoscaling/group). If <img style="margin:-3px 0;" src="https://main.qcloudimg.com/raw/df9771a6e2211e3f418ce257051313c3.png"> appears, the last scaling of the scaling group has failed.
>?Hover the cursor over the icon to view the cause of the exception.
>

## Problem Analysis
### Viewing the cause
Tencent Cloud AS provides the industry’s most intelligent method for viewing the cause of failed scaling group operations. Complete the following steps to view the details of a failure:
1. Click the **ID/Name** of the scaling group failed to be scaled in the [scaling group list](https://console.cloud.tencent.com/autoscaling/group).
2. On the details page of the scaling group, click **Scaling Activity** to view details, as shown in the following figure:
![](https://main.qcloudimg.com/raw/f6a022c51ec8ed3931efd5b7d3902aad.png)

### Troubleshooting based on the reasons
Troubleshoot the problems based on the cause of the failure as instructed below. Common causes of scaling failures are as follows:


### Causes of scaling failures
The causes of scaling failures are classified into the following types:
 - [CVM issues](#cvm)
 - [Image issues](#mirror)
 - [Network issues](#net)
 - [CBS issues](#cbs)
 - [CLB issues](#load)
 - [Other issues](#other)





## Troubleshooting

<span id="cvm"></span>
### CVM issues
#### 1. The CVM is sold out
Cause: the specified resource inventory is insufficient.
Solution: configure multi-model in the launch configuration, and select another instance specification and availability zone as needed.

#### 2. The CVM model is unavailable for the current availability zone
Cause: the specified instance specification is deactivated.
Solution: select an available instance specification in the launch configuration. For more information, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).

#### 3. The CVM and cloud disk does not match
Cause: the current system disk type does not support the instance model.
Solution: check the scaling configuration and change the system disk type. We recommend that you select Premium Cloud Storage or SSD disks.

#### 4. You are short of the CVM purchase quota
Cause: each user is assigned a CVM purchase quota. For the default quota of pay-as-you-go CVM instances, see [Purchase Limits for Pay-as-You-Go CVM Instances](https://intl.cloud.tencent.com/document/product/213/2664).
AS does not work for CVMs when this quota is exceeded..
Solution: decrease the number of CVMs for scale-out, or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for an increased quota.

#### 5. The CVM model does not exist
Cause: the model specified in the launch configuration is incorrect or deactivated.
Solution: modify the launch configuration.

<span id="mirror"></span>
### Image issues
#### 1. The image does not exist
Cause: the image does not exist or is invalid.
Solution: check the corresponding configuration in the launch configuration.

#### 2. The image size exceeds the system disk capacity
Cause: the system disk capacity is less than the image size.
Solution: check the launch configuration and increase the system disk capacity or use another image with a smaller size.

<sapn id="net"></span>
### Network issues
#### 1. Only VPC is supported
Cause: the model selected in the launch configuration only supports VPC.
Solution: do not use the model on the classic network. Deselect the model in the launch configuration.

#### 2. The number of IP addresses in the VPC subnet is less than the number of instances to be scaled out
Cause: the number of IP addresses in the VPC subnet is limited.
Solution: create a subnet and increase the IP range (CIDR block).


<sapn id="cbs"></span>
### CBS issues
#### 1. The cloud disks are sold out
Cause: the specified resource inventory is insufficient.
Solution: enable the default disk feature in the launch configuration.



#### 2. The CVM and cloud disk does not match
Cause: the current system disk type does not support the instance model.
Solution: check the scaling configuration and change the system disk type. We recommend that you select Premium Cloud Storage or SSD disks.

<sapn id="load"></span>
### CLB issues
#### 1. The CLB does not exist
Cause: the CLB does not exist or is invalid. Check the relevant configurations in the CLB.
Solution: ensure the CLB instance associated with the scaling group is running normally.


#### 2. The listener cannot be detected
Cause: the listener in the CLB does not exist or is invalid. Check the relevant configurations in the CLB.
Solution: ensure the CLB instance associated with the scaling group is running normally.

#### 3. The forwarding path does not exist
Cause: the forwarding domain name or URL of the listener in the CLB does not exist or is invalid. Check the relevant configurations in the CLB.
Solution: ensure the CLB instance associated with the scaling group is running normally.

#### 4. The specified CLB is busy
Cause: a CLB task is ongoing.
Solution: reduce manual operations for a scaling group during scaling to avoid mutual operation exclusion.

<sapn id="other"></span>
### Other issues
#### The lifecycle action is abandoned
Cause: a lifecycle hook for scale-out is configured for the scaling group. The hook is triggered during the scale-out of the scaling group and is finally rejected. As a result, the scaling operation is rolled back, and the scaled-out instance is released.
Solution: check the execution policy of the lifecycle hook.
