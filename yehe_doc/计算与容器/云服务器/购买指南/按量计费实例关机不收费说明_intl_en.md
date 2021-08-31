No Charges When Shut Down means you will not be charged for instances (CPU, memory) after you **select the No Charges When Shut Down option** to **shut down** pay-as-you-go instances. Components such as [cloud disks](https://intl.cloud.tencent.com/document/product/213/2255) (system disks and data disks), public network bandwidth (bill-by-bandwidth) and images will still be billed.

## Use Limits

The **No Charges When Shut Down** feature only applies to **pay-as-you-go instances** using **cloud disks as both system disk and data disk**.
The feature is **not available** for the following scenarios:
- You shutdown the instance after logging in to it, instead of shutting down it on the console.
- Mounting local disk instances.
- Spot instances.
- Instances that are shut down due to an overdue account: when an instance is shut down due to overdue payment, the billing for the instance and its associated resources stop. Computing resources and public IPs are released. The billing resumes after you pay the overdue payment.

If the batch shutdown operation includes instances that are eligible for No Charges When Shut Down and others that are not, then:
- For eligible instances, **CPU and memory will not be charged** after shutdown;
- Ineligible instances will **still be charged** after shutdown.

## Impacts

When the No Charges When Shut Down feature is enabled, it will cause the following impacts after instances are shut down.
1. After shutting down, the instance's CPU and memory **will not be retained**, so it **may fail** when restarted. If so, try restarting once more or wait awhile before retrying.
2. If the instance was assigned a public IP address, the public IP address will be **automatically released** after shutdown. A new public IP will be assigned when you restart the instance. The private IP remains the same. 
 **To retain the public IP, you can convert the public IP to an EIP before instance shutdown**. The EIP will be retained after instance shutdown as well as during restart, and no idle fee will be charged.
3. When the instance is shut down, most operations **except for instance startup** will not be available, including adjusting configurations, disks, and networks; reinstalling systems; restarting instances, resetting passwords; renaming, etc. **You will need to start the instance to perform those operations**.
4. No Charges When Shut Down **does not apply to** instance shutdown as a result of restarting the instance for configuration/disk adjustments, system reinstallation, and other OPS operations.

## Operations Guide

Please see [No Charges When Shut down for Pay-as-You-Go Instances Details](https://intl.cloud.tencent.com/document/product/213/19922).
