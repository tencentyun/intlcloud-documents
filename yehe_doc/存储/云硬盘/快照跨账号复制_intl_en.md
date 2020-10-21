The cross-account CBS snapshot replication is now available. With this feature, you can easily migrate data to another account, or build a cross-account disaster recovery system for cloud resources. This feature helps you maintain data integrity, even though an important snapshot under the current account is deleted accidentally. You can replicate snapshots using either of the following methods:
- [manual snapshot replication](#manual)
- [automatic snapshot replication](#auto)

>! The cross-account snapshot replication is currently in beta. If you want to try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Prerequisites

Because of the security and sensitivity of snapshot data, the following conditions must be met to replicate a snapshot:
- The account to which you replicate the snapshot must be a collaborator of your account. Refer to [Creating Collaborators](https://intl.cloud.tencent.com/document/product/598/32639) for details.
- The collaborator must be granted with the following action permissions. Refer to [Authorization](#Authorization) for details.
   - CopyAutoSnapshotPolicyCrossAccount
   - CopySnapshotCrossAccount

  

## Directions
<span id="manual"></span>
### Manual snapshot replication

You can quickly replicate a snapshot to another account which will save **full snapshot**. The detailed steps are as follows:
1. Log in to the CVM console and select [**Snapshot List**](https://console.cloud.tencent.com/cvm/snapshot) on the left sidebar to access the snapshot management page.
2. Locate the snapshot to be replicated, and click **More** -> **Cross-account Replication** in the **Operation** column.
3. In the pop-up window, complete the following configurations.
 - **Share to**: enter the unique ID of the account to which you want to replicate the snapshot.
 The collaborator needs to log in to the CVM console and click [Account Information](https://console.cloud.tencent.com/developer) in the upper-right corner to view the account ID in **Basic Information**.
 - **New snapshot name**: enter a name for the snapshot created from the replication. You can enter any name within 60 characters.
4. Click **OK** to start the replication. Hover over the information icon to view the status of the source snapshot. The new snapshot is added to the target account.

<span id="auto"></span>
### Automatic snapshot replication

If you want to build a cross-account disaster recovery system for cloud resources, you can use the automatic snapshot replication. To do this, you only need to associate the scheduled snapshot policy under the source account to the target account, the **full and incremental** snapshots subsequently created by the policy will be replicated to the target account. The detailed steps are as follows:
1. Log in to the CVM console and select [**Cross-account Auto-Replication**](https://console.cloud.tencent.com/cvm/snapshot/asp/inter-account?rid=19&tab=REMOTE) on the left sidebar to access the snapshot management page.
2. Click **Create**.
3. In the pop-up window, enter the unique account ID for **Share to**, select the scheduled snapshot policy, and click **OK**.
 - You can view this task on the [**Replicate to other account**](https://console.cloud.tencent.com/cvm/snapshot/asp/inter-account?rid=19&tab=REMOTE) page for the source account. The auto-replication has the same lifecycle as the associated scheduled snapshot policy, which will automatically stop if the policy is deleted.
 - You can view this task on the [**Replicate to my account**](https://console.cloud.tencent.com/cvm/snapshot/asp/inter-account?rid=19&tab=LOCAL) page for the target account. The auto-replication can be deleted by the target account.


## Relevant Operations
<span id="Authorization"></span>

### Authorization
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









