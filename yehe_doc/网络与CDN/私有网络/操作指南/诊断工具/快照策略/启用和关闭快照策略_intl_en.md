A successfully created snapshot policy is enabled by default. This document describes how to disable and enable it again when needed. Disabling it will stop generating snapshot backups of all its associated security groups without deleting the original backup information.

## Disabling Policy
After the policy is disabled, no more backups will be performed but the original backup information will not be deleted.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/) and select **Diagnostic Tools** > **Snapshot Policy** on the left sidebar.
2. On the **Snapshot Policy** page, click the snapshot policy ID to enter the details page. The blue toggle button in the figure indicates that the policy is enabled.
<img src="" width="60%">
3. Click the button, confirm the impact in the **Disable Snapshot Policy** pop-up window, and click **OK**.
<img src="" width="60%"> 
The disabled policy is as shown below:</br>
<img src="" width="60%">


## Enabling Policy
After the policy is disabled, you can enable it again as instructed below. Then the associated security group rules will continue to be backed up according to the previously configured policy.
1. Click the **Enable Policy** toggle.
2. In the **Enable Snapshot Policy** pop-up window, click **OK**.
