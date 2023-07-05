This document describes how to terminate and release a Cloud Virtual Machine (CVM) instance. For more information on expiration, see [Payment Overdue](https://intl.cloud.tencent.com/document/product/213/2181).

## Overview

You can terminate an instance if you no longer need it. The terminated instance will be put into the recycle bin. For instances in the recycle bin, you can restore or release them as needed based on different scenarios.


<dx-alert infotype="notice" title="">
If your account is in arrears, then for pay-as-you-go instances, you need to renew the instances first before restoring them.
</dx-alert>



## Methods for Termination/Release
For pay-as-you-go instances, the methods for instance termination and release are as follows:
 - **Manual termination:** You can manually terminate a pay-as-you-go instance that is not in arrears. A pay-as-you-go instance is released after it remains in the recycle bin for over 2 hours.
 - **Timed termination:** Timed termination is supported for pay-as-you-go instances. You can select a future time to terminate resources. The set termination time is precise to the second. Instance resources for which timed termination is set will be released immediately as scheduled, instead of going into the recycle bin. You can [cancel timed termination](https://intl.cloud.tencent.com/document/product/213/46012?has_map=1#.E6.92.A4.E9.94.80.E5.AE.9A.E6.97.B6.E9.94.80.E6.AF.81) at any time before the set termination time.
 - **Expiry/arrears auto termination:** Pay-as-you-go instance will be automatically terminated when its balance drops below 0 for 2 hours and 15 days. Billing will continue for the first 2 hours, then the instance will shut down and no longer be billed. The pay-as-you-go instance in arrears will not enter the recycle bin and can be viewed on the instance list. You can continue to use the instance if you renew it within the specified time. For more information, see [Renewing Instances](https://intl.cloud.tencent.com/document/product/213/6143).

|  | Manual termination (not in arrears) | Timed termination (not in arrears) | Automatic termination upon expiration or when in arrears |
|---------|---------|---------|---------|
| Pay-as-you-go instances | After termination, the instance is stored in the recycle bin for 2 hours, and if it is not restored within these 2 hours, it will be released. | Instances for which timed termination is set will be released immediately as scheduled, instead of going into the recycle bin. | After an instance enters into arrears, for the first 2 hours, billing will continue and the instance can still be used normally. In the next 15 days, however, the instance will be shut down, and billing will stop. Pay-as-you-go instances in arrears will not be put into the recycle bin. If the instance is not renewed within the aforementioned period, the instance will be released. |


## Relevant Impact
When an instance is terminated, the relevant impact on instance data, EIPs, and billing is as follows:
- **Billing:** when an instance is being terminated or has been released, no expenses related to this instance are incurred.
- **Instance data:** local disks and non-elastic cloud disks attached to the instance are all released, and the data on these disks will be lost. Back up the data in advance. Elastic cloud disks follow their own lifecycle.
- **EIP:** EIPs (including IP addresses on the secondary ENI) of a terminated instance are retained, and idle IP addresses may incur expenses. If you don't need them anymore, release them as soon as possible.

## Directions
You can manually terminate/release instances through the following ways:
- Terminate/release instances in the console. For more information, see [Terminating/Returning Instance in Console](https://intl.cloud.tencent.com/document/product/213/46012).
- Terminate/release instances by calling the API. For more information, see [TerminateInstances](https://intl.cloud.tencent.com/document/product/213/33234)

