This document describes how to delete a snapshot policy if you no longer need to generate snapshot backups of security group rules but need to delete the backup records of all security group rules associated with the snapshot policy.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/) and select **Diagnostic Tools** > **Snapshot Policy** on the left sidebar.
2. On the **Snapshot Policy** page, click **Delete** on the right of the target snapshot policy.
3. In the confirmation pop-up window, confirm the impact and click **OK**.
<dx-alert infotype="notice" title="">
Note that after the deletion, all security group rules associated with the snapshot policy will no longer be backed up, and the existing backup records will be deleted.
</dx-alert>

