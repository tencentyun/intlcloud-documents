### What is the cooldown period?
The cooldown period refers to the locking duration after one scaling activity (the addition or removal of CVMs) is executed in a scaling group. During which, the scaling group performs no scaling activities. You can optionally set the cooldown period to a value less than 999,999 seconds.

### Do manually added CVMs have a cooldown period?
No.

### Is there a charge for Auto Scaling?
No. The Auto Scaling feature is completely free of charge. Please feel free to use it.
CVM instances that are automatically created through auto scaling are billed the same as pay-as-you-go CVMs. Manually added CVM instances are charged by their original billing policy, and immune to scaling activities.

### How do I increase the maximum number of CVMs in the scaling group?
One scaling group can have a maximum of 2,000 CVMs. For more information about the current quota of pay-as-you-go CVMs under an account in each availability zone, see “Purchase Limits for Pay-as-You-Go CVM Instances” under [Purchase Limits](https://intl.cloud.tencent.com/document/product/213/2664). If you want to have more than 2,000 CVMs in one scaling group, or if you want to use more pay-as-you-go CVMs than the fixed quota, [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&source=0).

### What kinds of servers are suitable for Auto Scaling?
Applications that are deployed in the CVM instances in the scaling group should be stateless and replaceable. Because instances in the scaling group are likely to be repossessed by Tencent Cloud during scale-in, CVM instances for Auto Scaling cannot save the status information (such as sessions) and data (such as databases and logs) of the applications. If you need to save the status information in your application, you can consider saving it in a standalone CVM outside the scaling group.

### What kinds of CVMs can be manually added to the scaling group?
A CVM that is manually added to the scaling group must meet the following requirements:
- In the same region as the scaling group.
- In the same network environment (VPC or classic network) as the scaling group.
- In a normal running status.

### What kinds of CLB instances can be associated with the scaling group?
A CLB instance (in the case of a cross-region CLB instance, its backend instance VPC) that is associated with a scaling group must be in the same network environment (VPC or the classic network of the same region) as the scaling group.


### Can Auto Scaling automatically upgrade or degrade the configurations of CVMs?
No. Auto Scaling is a management service that elastically adjusts computing resources according to your business needs and policies. It can automatically add CVM instances when the business grows and remove CVM instances when the business declines. Currently, Auto Scaling does not support "scaling up", that is, Auto Scaling cannot automatically change the CPU, memory and bandwidth of CVMs.

### Does Auto Scaling have to work with CLB and Cloud Monitor?
No. Auto Scaling can independently scale CVM instances out and in. It can work with CLB or work alone.

### What should I do to add CVMs during a specific period of time?
You can configure two scheduled actions: one defines the desired capacity of scale-out, and the other defines the desired capacity of scale-in.

### What are the specific rules for removing CVMs from the scaling group?
Tencent Cloud Auto Scaling provides two removal policies:
- Remove the earliest: remove the earliest instances in the group. Instances added automatically are removed first, and then the manually added ones.
- Remove the latest: remove the latest instances in the group. Instances added automatically are removed first, and then the manually added ones.

### How does the alarm policy collect the cloud monitoring information?
Take the maximum value as an example. It collects one sample per minute from each CVM in the period. If the sample value meets the configured rules for multiple periods consecutively (the number of periods can be customized), the alarm scaling action will be triggered.

For example: there are five CVMs in a scaling group, and the defined alarm scaling policy is “CPU utilization exceeds 50% for 3 consecutive periods”. The system takes one value per minute from each CVM, that is, it takes 25 CPU utilization values within one period (5 minutes). If there are values exceeding 50% for 3 consecutive periods, the scaling rule is satisfied and scaling actions are triggered.

### What is the desired capacity?
The desired capacity is the reasonable number of instances in the current scaling group. Its value should be between the minimum and maximum capacity. You can manually adjust the desired capacity, and you can also use scheduled action and alarm scaling task to trigger adjustment. The scaling group automatically adjusts the actual number of instances to match the desired capacity.
- Configure on scaling group creation: if you set an initial capacity when creating the scaling group, then the desired capacity will be the initial capacity.
- Adjusted by alarm scaling task: when alarm scaling is triggered, the scaling group will adjust the current number of instances to the desired capacity. For example, if the triggered action is to add two CVMs, the backend will add two CVMs to the current number to achieve this. If the system finds that the current number of instances of the scaling group is not equal to the desired capacity, it will add two CVMs to make them equal.
- Adjusted manually or by scheduled actions: if the desired capacity was modified manually or through a scheduled action, and the system finds that the current number of instances is not equal to the desired capacity, the system will trigger a scaling action to make the number equal to the desired capacity.
- Automatically adjusted: the desired capacity should be between the maximum and minimum capacity. If the maximum or minimum capacity changes, this may result in a change to the desired capacity. For example, assume that the desired capacity is 3, the minimum capacity is 2 and the maximum capacity is 5. If the minimum capacity is adjusted to 4, then the desired capacity will be adjusted to 4 to match the minimum capacity.

### What should be noted when a data disk snapshot is specified in the launch configuration?
If the launch configuration specifies a data disk snapshot, you must ensure that the data disk can be automatically mounted to ensure proper auto scale-out. Please configure the source instance of the snapshot as instructed below:
[Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).

### What will happen when the scaling group is disabled?
After the scaling group is disabled, automatically triggered actions will not proceed, but restrictions on the scaling group are still effective.
After the scaling group is disabled, the following automatic actions will not proceed:
- Alarm scaling
- Scheduled actions
- Health checks
- Matching the current number of CVMs with the desired capacity

To ensure the normal running of the business, manual scaling is still available, with the following restrictions:
- If the number of instances is less than the `min` capacity, the removal will not be allowed.
- If the number of instances is greater than the `max` capacity, the addition will not be allowed.
- Increasing the `min` or `max` capacity manually will not trigger a scaling action.

### What stages are involved in the lifecycle of the CVMs that are automatically added to a scaling group?
- Creating: the CVM is being created
- InService: the CVM is in service
- Removing: the CVM is being removed
- Attaching: the CVM is being bound to the scaling group
- Detaching: the CVM is being unbound from the scaling group
- AttachLb: the CVM is being bound to a LB
- DetachLb: the CVM is being unbound from a LB
- Preheating: the CVM is preheating


### What are the rules for CVM removal?
- Removal of a manually added CVM: the CVM is only removed from the scaling group but not terminated. Auto Scaling will unbind the CVM from the LB that was automatically bound at the time of joining the scaling group, but the LB manually bound will not be unbound.
- Removal of an automatically created CVM: the CVM will be terminated and unbound from the LB.
