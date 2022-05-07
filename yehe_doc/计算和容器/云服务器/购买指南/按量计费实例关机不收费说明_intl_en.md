No Charges When Shut Down means you will not be charged for instances (CPU, memory) after you select the **No Charges When Shut Down** option to **shut down** pay-as-you-go instances. Components such as [cloud disks](https://intl.cloud.tencent.com/document/product/213/2255) (system disks and data disks) and images will still be billed.


## Usage Limits
- **No Charges When Shut Down** only applies to **pay-as-you-go instances** whose **system disk and data disks are both cloud disks**.
- This option is **not available** in the following scenarios:
	- Starting up/shutting down an instance after login.
	- Instances attached with local disks.
	- Spot instances.
	- Instances that are shut down due to overdue payment: the billing for instance and associated resources stops after they are shut down due to overdue payment. Computing resources and public IPs will be released. The billing will resume after payment is made.
- During the No Charges When Shut Down period, pay-as-you-go instances support for the tiered pricing (see [Billing Overview](https://intl.cloud.tencent.com/document/product/213/2176)) no longer calculate the usage period. After the instance is restarted, its usage period will continue to count.
- If a batch shutdown operation involve instances that are eligible for no charges when shut down and others that are not, then:
	- For eligible instances, **CPU and memory will not be charged** after shutdown;
	- Ineligible instances will **still be charged** after shutdown.

## Impacts

When the No Charges When Shut Down feature is enabled, it will **affect** instances as follows:
1. After the instance is shut down, its CPU and memory **will be released**, and starting it again **may fail** due to insufficient resources. If the instance fails to be started, try starting it once more later. If the starting still fails, try other instance specifications. For more information, see [Changing Instance Configuration](https://intl.cloud.tencent.com/document/product/213/2178).
2. If the instance was assigned a public IP address, this IP will be **automatically released** after shutdown. Therefore, the instance might fail when restarted. After the instance is restarted, a new public IP will be assigned, while the private IP remains the same.
 **To retain the public IP, you can convert it to an EIP before shutting down an instance**. After the CVM is shut down, the EIP will be retained and stop incurring charges.
3. When the instance is shut down, most operations **except for instance startup** will not be available, including adjusting configurations, disks, and networks; reinstalling systems; restarting instances; resetting passwords; renewing; renaming, etc. **You need to start the instance to perform those operations**.
4. No Charges When Shut Down **does not apply to** instance shutdown as a result of configuration/disk adjustments, system reinstallation, and other OPS operations.

## Operation Guide

For more information, see [No Charges When Shut Down for Pay-as-You-Go Instances](https://intl.cloud.tencent.com/document/product/213/19922).
