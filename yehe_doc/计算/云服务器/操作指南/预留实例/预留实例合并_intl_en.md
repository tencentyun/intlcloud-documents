## Overview
You can merge multiple reserved instances into a single reserved instance with a larger [normalization factor](#length), so as to apply it to larger on-demand instances.

## Rules and Limits
● The original reserved instances are in the **Activated** status.
● The original reserved instances are in the same availability zone.
● The payment methods for the original reserved instances are the same.
● The original reserved instances have the same operating system (Windows/Linux) and expiration time.
● Merging the 1C1G, 1C2G, and 2C4G reserved instances is not supported.
● You can modify the instance size but not the instance family.
● Modifying the region or availability zone of a reserved instance is not supported.
● The total normalization factors of destination reserved instances must be equal to that of the original reserved instance.
● Make sure the CPU:MEM ratio is the same before merging.

## Directions
1. Log in to the CVM console;
2. Click **Reserved Instances** in the left sidebar;
3. On the **Reserved Instances** page, find the original reserved instances and click **Merge** under the **Operation** column;
4. In the pop-up window, select the reserved instances to be merged, and enter a new name for the destination reserved instance.

## Execution Result
After merging, the original reserved instances enter the **Expired** status, while the new reserved instance is in **Activated** status.

## <a id="length">Definitions</a>
Normalization factor: It indicates the CPU performance of an instance. For the splitting and merging of reserved instances, the normalization factor is calculated based on the number of vCPUs.
Sum of normalization factor = Normalization factor of the instance size × Instance quantity. The sum of normalization factors must keep the same as the one before splitting.
