## Overview
You can split a reserved instance into multiple reserved instances with smaller [normalization factors](#length), and apply them to smaller on-demand instances.

## Rules and Limits
● 1C1G, 1C2G, and 2C4G reserved instances cannot be split.
● You can change the instance size, but not the instance type.
● The region and availability zone cannot be changed.
● The sum of normalization factors cannot be changed.
● Make sure the CPU:MEM ratio is the same before splitting;
● One reserved instance can be split into a maximum of 100 reserved instances.

## Directions
1. Log in to the CVM console;
2. Click **Reserved Instances** in the left sidebar;
3. On the **Reserved Instances** page, find the original reserved instance and click **Split** under the **Operation** column;
4. In the pop-up window, configure the name, CPU, memory and quantity of new reserved instances.

## Execution Result
After splitting, the original reserved instance goes to the **Expired** status, while the new reserved instances are in **Activated** status.

## <a id="length">Definitions</a>
Normalization factor: It indicates the CPU performance of a For the splitting and merging of reserved instances, the normalization factor is calculated based on the number of vCPUs.
Sum of normalization factor = Normalization factor of the instance size × Instance quantity. The sum of normalization factors must keep the same as the one before splitting.
