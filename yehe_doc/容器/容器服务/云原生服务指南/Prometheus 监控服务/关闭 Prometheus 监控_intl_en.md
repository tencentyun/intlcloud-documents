## Overview

If you no longer need to use TMP to monitor clusters, you can delete all monitoring instances in the TMP console. The system will automatically uninstall the monitoring add-on and terminate relevant resources.



## Directions

1. Log in to the **TKE console** and select **TMP** on the left sidebar.
2. On the instance list page, find the target instance and click **Terminate/Return** on the right.
3. In the **Terminate/Return** pop-up window, confirm the instance information and click **OK**.
<dx-alert infotype="explain" title=" ">
- After an instance is deleted, the TMP console will no longer display its information.
- After an instance is deleted, its resources (such as monitoring add-on) and configurations will be deleted, the associated cluster will be automatically disassociated and no longer be monitored, and the associated EKS cluster will be deleted.
- Note that the instance data cannot be recovered after the deletion. Proceed with caution.
</dx-alert>



