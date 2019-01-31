With "No Charges When Shut Down" enabled, users don't need to pay for Pay-as-you-go instances (CPUs, memory) that are **shut down** by themselves. However other resources bound with these instances, like cloud disks (system disk, data disk), public network bandwidth and images, are still charged.

## Use Limits
**No charges when shut down** only applies to **Pay-as-you-go instances** that using cloud disk as **system disk and data disk**.
This feature is **not available** in the following cases:

- The instance is shut down in its own operation system  
- The instance is mounted with local disks
- GPU- and FPGA-based instances
- Instance is shut down due to account in arrears. In this case, the instance and associated resources are suspended and not charged. The computing resource and public IP are released. Billing of all resources resumes after the arrears are paid.

In case multiple instances are selected, some of them are available for No Charges When Shut Down while the rest are not:

- For the available ones, they are **not charged for CPU and memory** when the they're shut down;
- For the unavailable ones, they are **still charged** when they're shut down.

## Impacts
IMPORTANT: Read the following impacts carefully before enabling No Charges When Shut Down:

1. The instance's CPU and memory **will not be retained** when it's shut down. Hence **it may fail** when you restart it. In this case, please try to start it again instantly or later. 
2. The public IP bound with the instance **will be released** when it's shut down. A new public IP is assigned when you restart the instance. However, its private IP remains unchanged. **To retain the public IP, you can convert the public IP to an EIP before shutting down the instance**. EIP is retained when you shut down and restart the instance, and no idle fee is charged.
3. When the instance is shut down, **most operations are not available**, including adjusting configuration/disks/network, reinstalling system, restarting instance, resetting password, renewing, etc. You need to **start up the instance** for these operations.
4. For instances that are shut down for adjusting configuration/disks, reinstalling system and other OPS operations, No Charges When Shut Down is **unavailable**.

## Operation Guide
For more information, please see [No Charges When Shut Down for the Pay as You Go Instance](https://cloud.tencent.com/document/product/213/19922)
