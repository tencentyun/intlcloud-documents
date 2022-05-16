CBS supports replication of snapshots across regions, allowing you to easily migrate data to another account. With this feature, you can build up a cross-account disaster recovery system for cloud resources, so as to prevent data loss caused by mis-operation of an account. You can replicate snapshots using either of the following methods:
- [Manual snapshot replication](#manual)
- [Automatic snapshot replication](#auto)

<dx-alert infotype="notice" title="">
The cross-account snapshot replication is in beta test. If you want to try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
</dx-alert>



## Prerequisite

For security reasons, the following conditions must be met to replicate a snapshot:
- The destination account must be a collaborator of your account. Refer to [Creating Collaborator](https://intl.cloud.tencent.com/document/product/598/32639) for details.
- The collaborator must be granted with the following action permissions. Refer to [Authorization](#Authorization) for details.
   - CopyAutoSnapshotPolicyCrossAccount
   - CopySnapshotCrossAccount

  

## Directions
### Manual replication[](id:manual)

You can replicate a snapshot to another account which will save **full snapshot**. The detailed steps are as follows:
1. Log in to the CVM console and select **[Snapshot List](https://console.cloud.tencent.com/cvm/snapshot)** on the left sidebar to access the snapshot management page.
2. Locate the snapshot to be replicated, and click **More** > **Cross-account Replication** under the **Operation** column.

3. In the pop-up window, complete the following configurations.
 - **Share to**: Enter the unique ID of the destination account.
 The collaborator needs to log in to the CVM console and click [Account Information](https://console.cloud.tencent.com/developer) in the upper-right corner to view the account ID in **Basic Information**.
 - **New snapshot name**: Enter a name for the snapshot created from the replication. You can enter any name within 60 characters.
4. Click **OK** to start the replication. Hover over the information icon to view the status of the source snapshot. The new snapshot is added to the target account.


### Automatic replication[](id:#auto)

If you want to build a cross-account disaster recovery system for cloud resources, you can use the automatic snapshot replication. To do this, you only need to associate the scheduled snapshot policy under the source account to the destination account, the **full and incremental** snapshots subsequently created by the policy will be replicated to the target account. The detailed steps are as follows:
1. Log in to the CVM console and select **[Cross-account Auto-Replication**](https://console.cloud.tencent.com/cvm/snapshot/asp/inter-account?rid=19&tab=REMOTE)** on the left sidebar to access the snapshot management page.
2. Click **Create**.
3. In the pop-up window, enter the unique ID of destination account, select the scheduled snapshot policy, and click **OK**.
 - You can view this task on the [**Replicate to other account**](https://console.cloud.tencent.com/cvm/snapshot/asp/inter-account?rid=19&tab=REMOTE) page for the source account. The auto-replication has the same lifecycle as the associated scheduled snapshot policy, which will automatically stop if the policy is deleted.
 - You can view this task on the [**Replicate to my account**](https://console.cloud.tencent.com/cvm/snapshot/asp/inter-account?rid=19&tab=LOCAL) page for the destination account. The auto-replication can be deleted by the destination account.


## Operations

### Authorization[](id:Authorization)
Perform the following steps to grant the action permissions to the collaborator:
1. [Create a custom policy](https://intl.cloud.tencent.com/document/product/598/35596) by policy syntax. The following sample codes show a complete policy.
```
   {
       "version": "2.0",
       "statement": [
           {
               "action": [
                   "cvm:*Cbs*",
                   "cvm:*Storage*",
                   "cvm:*Snapshot*"
               ],
               "resource": "*",
               "effect": "allow"
           }
       ]
   }
```
2. Authorize the policy to the collaborator. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).









