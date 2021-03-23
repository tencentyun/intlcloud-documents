
## Operation Scenario
This document describes how to terminate and return Enterprise Edition instances in Tencent Container Registry (TCR).

## Prerequisites
You have [purchased a TCR Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088), and the current account has permission to delete that instance.


## Directions
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr/instance?rid=1).
2. Select **Instance List** in the left sidebar to go to the "Instance List" page.
   ![](https://main.qcloudimg.com/raw/153c64557e77527b45977033511da837.png)
3. Click **Delete** to the right of the instance that you want to delete.
4. In the confirmation window that pops up, you can select "Delete the associated COS bucket with the instance" based on your needs, as shown in the figure below:
![](https://main.qcloudimg.com/raw/61aae8be9dd0bd6f9be1f03ccdeced30.png)
 >! 
 >- Please read the instance deletion prompts carefully. Deleting an instance will completely and irrecoverably erase the user data and relevant configuration stored during the use of the instance. Please exercise caution.
 >- If you are sure that you no longer need the container images, Helm Charts, and other underlying data stored during the use of the TCR Enterprise Edition instance, you can select "Delete the associated COS bucket with the instance" to avoid unnecessary fees.
 >- If the current account is overdue, the COS service does not allow you to directly delete the associated COS bucket. Therefore, do not select that option. In that case, after normally deleting an instance, go to the [COS console](https://console.cloud.tencent.com/cos) to manage the COS bucket.

5. Click **OK** to delete the currently selected instance. No fees will be charged for this instance after deletion.

>? If it takes too long to delete an instance or the displayed status is abnormal, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
