"No Charge During Shutdown" means you won't be charged for pay-as-you-go instances (CPUs and memory) that were shut down. Cloud disks (system disk and data disk), public network bandwidth and images will still be billed.

## Usage Restrictions
**No Charges when Shut down** only applies to **Pay-as-You-Go instances** that using cloud disk as both **system disk and data disk**.
This feature is **not available** in the following cases:

- The instance is shut down within its own operating system  
- The instance is mounted with local disks
- GPU- and FPGA-based instances
- Instance is shut down due to account in arrears. In this case, the instance and associated resources are suspended and not charged. The computing resource and public IP will be released. Billing of all resources resumes after the arrears are paid.

In cases where multiple instances are selected and some of them are eligible for No Charges When Shut Down while the rest are not:

- For those that are eligible, they are **not charged for CPU and memory** when they are shut down;
- For those that are ineligible, they are **still charged** when they are shut down.

## Impacts
IMPORTANT: Read the following impacts carefully before enabling the "No Charges When Shut Down" feature:

1. The instance's CPU and memory **will not be retained** when it is shut down. Hence **it may fail** when you restart it. In this case, please try to start it again instantly or later. 
2. The public IP bound with the instance **will be automatically released** when it is shut down. A new public IP is assigned when you restart the instance. However, its private IP remains unchanged. **To retain the public IP, you can convert the public IP to an EIP before shutting down the instance**. EIP is retained when you shut down and restart the instance, and no idle fee is charged.
3. When the instance is shut down, **most operations are not available**, including adjusting configuration/disks/network, reinstalling system, restarting instance, resetting password, renewing, etc. You need to **start up the instance** for these operations.
4. Instances that are shut down for adjusting configuration/disks, reinstalling system and other OPS operations are **ineligible** for the "No Charges When Shut Down" feature.

## Operation Guide
For more information, please see [No Charges When Shut Down for Pay-as-You-Go Instances](https://intl.cloud.tencent.com/document/product/213/19922)
