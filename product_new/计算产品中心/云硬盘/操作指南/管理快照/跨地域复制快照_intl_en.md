Cross-region snapshot replication is now in beta test. With this feature, you can easily migrate data and services to other regions, or build a cross-region disaster recovery system for your business.
You can [submit an application](https://cloud.tencent.com/act/apply/snapshotcopy) to use this feature.

## Use Limits
- **Whitelisted User Only**: Cross-region snapshot replication is now in beta test. You need to [submit an application](https://cloud.tencent.com/act/apply/snapshotcopy) to use this feature.
- **Supported Regions**: For the time being, this feature is available in Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Bombay, and Guangzhou Open. We will provide this feature to all regions soon.
- **Snapshot Rollback**: The snapshot created through cross-region snapshot replication is not associated with the source disk. Therefore, the rollback feature is not available for the new replicated snapshot.

## Directions
1. Access the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page.
2. Click **Cross-Region Replication** for the target snapshot.
3. Configure the following parameters:
  - New snapshot name: Enter the new snapshot name, which is a string of up to 60 characters. This parameter is optional.
    By default, a new snapshot name contains the source snapshot ID and region information and is in the following format: `Copied <Source snapshot ID> from <Source snapshot region>`, for example, `Copied snap-oi5spwt2 from ap-shanghai`.
  - Region: (Required) Select the destination region.
    Please check the snapshot quota and geographical restriction when you select the region.

 ![1](https://main.qcloudimg.com/raw/81bc5c94ed8a5ae1b699f0a527322102.png)
4. Click **Confirm** to start the replication. Hover over the information icon to view the status of the source snapshot. The new snapshot is added to the destination region. Once the replication is completed, you can view the new snapshot in the snapshot list of the destination region.
> The source snapshot cannot be deleted during the cross-region replication of this snapshot.
>
 - The following figure shows the status of the source snapshot during cross-region replication:
![2](https://main.qcloudimg.com/raw/27d6bfa6389efc75d17c4a1c3d4d1899.png)
 - The following figure shows the status of the snapshot created during cross-region replication:
![3](https://main.qcloudimg.com/raw/0564debf0293e79907dedf7ee7fe02a9.png)
