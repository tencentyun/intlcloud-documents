
Log into the [Auto Scaling Console](https://console.cloud.tencent.com/autoscaling), and select **Scaling Group** in the left sidebar.

Select the scaling group to be modified, and click the scaling group’s ID to go to the basic information page.
![](https://main.qcloudimg.com/raw/6c9d3876e1d343ae8ddd6fc2ad912112.png)

You can view the list of CVMs that are bound to the scaling group in this page.
- To manually add CVM instances to the scaling group, click **Add CVM**, select the instance to be added (hold the Shift key to select multiple instances) and click **OK**.
- To unbind a specific CVM, click **Remove** at the end of the corresponding CVM entry.
![](https://main.qcloudimg.com/raw/2c4c7f20ccfbb5b72588aaaf3d61a7ba.png)

CVM that automatically created in scale-out event will be terminated when they’re removed from the scaling group.
Manually added CVMs will not be terminated upon removal. They will only be removed from the scaling group, and the Cloud Load Balancer will be unbound.
