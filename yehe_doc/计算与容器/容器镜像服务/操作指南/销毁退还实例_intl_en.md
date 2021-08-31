
## Overview
This document introduces how to terminate or return Enterprise Edition instances in Tencent Container Registry (TCR).

## Prerequisites
You have [purchased a TCR Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088), and the current account has the permissions to delete this instance.


## Directions
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr/instance?rid=1).
2. Select **Instance** in the left sidebar to go to the "Instance List" page.
3. Select **More** > **Terminate/Return** on the right side of the instance that needs to be terminated or returned.
4. In the confirmation window that pops up, you can select **Delete associated COS Bucket** based on your needs, as shown in the figure below:
![](https://main.qcloudimg.com/raw/d6dbb8b3a6765d8372b51ce55dd5a8f6.png)
<dx-alert infotype="notice" title="">
- Please read the notes for terminating and returning the instance carefully. Deleting an instance will completely and irrecoverably erase the user data and relevant configuration stored during the use of the instance.
- If you are sure that you no longer need the container images, Helm Charts, and other underlying data stored during the use of the TCR Enterprise Edition, you can select **Delete associated COS Bucket** to avoid unnecessary fees.
- If the current account has overdue payment, the COS service does not allow you to directly delete the associated COS bucket. Therefore, do not select that option. In that case, after normally deleting an instance, go to the [COS console](https://console.cloud.tencent.com/cos) to manage the COS Bucket.
- The billing of pay-as-you-go instances stops once they're terminated.
</dx-alert>
5. Select **I have read and agreed to Refund Rules** and click **Confirm** to delete the instance. No fees will be charged for this instance after deletion.
<dx-alert infotype="explain" title="">
If it takes too long to delete an instance or the displayed status is abnormal, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
</dx-alert>



## Reference

You can also use the `DeleteInstance` API to delete the instance. For more information, see DeleteInstance API Documentation.
