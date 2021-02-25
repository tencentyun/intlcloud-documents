## Scenario
This document describes how to manage spread placement groups.For more information about the placement group, see [Placement Group](https://intl.cloud.tencent.com/document/product/213/15486).

## Directions
### Creating a placement group

1. Log in to the [CVM placement group console](https://console.cloud.tencent.com/cvm/ps).
2. Click **Create**.
3. In the window that appears, enter a name for the placement group, and select the layer of the placement group.
4. Click **OK** to finish the creation.

### Starting up an instance in the placement group
1. Go to the [CVM purchase page](https://buy.cloud.tencent.com/?tab=custom&step=1&devPayMode=hourly&regionId=33&instanceType=SA2.SMALL1&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR).
2. Complete the purchase as prompted on the page.
During the purchase process, be sure to perform the following operations:
 - When setting the CVM, click **Advanced Configuration**, select **Add Instance to Placement Group**, and select an existing placement group.
 If no existing placement groups meet your requirement, [create one](https://console.cloud.tencent.com/cvm/ps?regionId=1) in the console.
 - When confirming the configuration information, enter the total number of instances to be added to the placement group, which must be less than the quantity limit set for the placement group.


### Modifying an instance's placement group
> Currently, you can change only the name of a placement group. To do this, complete the following steps.
>
1. Log in to the [CVM placement group console](https://console.cloud.tencent.com/cvm/ps).
2. Hover the cursor over the ID or name of the target placement group and click <img src="https://main.qcloudimg.com/raw/beb5eae230dc169f7274bda7a19a5aa6.png" style="margin: 0;"></img>.
3. In the window that appears, enter the new name.
4. Click **OK** to finish the modification.

### Deleting a placement group
> You can delete a placement group that needs to be replaced or is no longer needed. You must terminate all instances running in the placement group before you can delete it. To do this, complete the following steps.
>
1. Log in to the [CVM placement group console](https://console.cloud.tencent.com/cvm/ps).
2. Click **Number of Instances** for the placement group to be deleted to go to the instance management page, and terminate all instances in the placement group.
3. Return to the placement group console, select the placement group to be deleted, and click **Delete**.
6. In the window that appears, click **OK** to finish the deletion.
You can delete a single placement group or multiple placement groups in batches.
