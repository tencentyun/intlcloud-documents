"No Charges When Shut Down" means you won't be charged for pay-as-you-go instances (CPUs and memory) that are shut down. Cloud disks (system disk and data disk), public network bandwidth and images will still be billed.

## Usage Restrictions
**No Charges When Shut Down** feature only applies to **pay-as-you-go instances** using cloud disk as both **system disk and data disk**.
The feature is **not available** for the following scenarios:

- The instance is shut down within its own operating system  
- The instance is mounted with local disks
- GPU- and FPGA-based instances
- Instance is shut down due to account in arrears. Instance, associated resources and billing will be suspended. Computing resources and public IPs will be released. Billing resumes after arrears are paid.

If multiple instances are selected and some are eligible for No Charges When Shut Down while the others are not, then:

- For eligible instances, **CPU and memory will not be charged** after shutdown;
- For ineligible instances, they will**still be charged** after shutdown.

## Impacts
IMPORTANT: Read the following notes carefully before enabling "No Charges When Shut Down" feature:

1. Instance's CPU and memory **will not be retained**. Therefore, **it may fail** when you restart. You can try again or try later.
2. Public IP bound with instance **will be released automatically** after shutdown. A new public IP will be assigned when you restart the instance. Private IP remains the same.  **To retain the public IP, you can convert the public IP to an EIP before instance shutdown**. EIP will be retained after instance shutdown and restart, and no idle fee will be charged.
3. When the instance is shut down, **most operations will not be available**, including adjusting configuration/disks/network, reinstalling system, restarting instance, resetting password, renewing, etc. You need to **restart instance** to conduct those operations.
4. "No Charges When Shut Down" does not apply to instance shutdown as a result of configuration/disks adjustments, system reinstallation and other OPS operations.

## Operation Guide
For more information, see [No Charges When Shut Down Pay-as-You-Go Instance](https://intl.cloud.tencent.com/document/product/213/19922)
