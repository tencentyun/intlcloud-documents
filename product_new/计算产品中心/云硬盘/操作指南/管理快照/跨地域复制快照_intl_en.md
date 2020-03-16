Cross-region snapshot replication is now in beta. With this feature, you can easily migrate data and services to other regions, or build a cross-region disaster recovery system for your business.
You can [submit an application](https://console.cloud.tencent.com/act/apply/snapshotcopy) to use this feature.

## Use Limits
- **Apply for Beta**: cross-region snapshot replication is now in beta. You need to [submit an application](https://cloud.tencent.com/act/apply/snapshotcopy) to apply for it.
- **Supported regions**: for more information, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/362/32396)。


## Directions

1. Log in to the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page.
2. Click **Cross-Region Replication** for the target snapshot.
3. Configure the following parameters:
  - **New snapshot name**: (optional) enter the new snapshot name with up to 60 characters.
    By default, a new snapshot name contains the source snapshot ID and region information and is in the following format: `Copied <Source snapshot ID> from <Source snapshot region>`, for example, `Copied snap-oi5spwt2 from ap-shanghai`.
  - **Region**: (required) a target region to which a snapshot is copied
    Please check the snapshot quota and geographical restriction when you select the region.
4. Click **OK** to start the replication. Hover over the information icon to view the status of the source snapshot. The new snapshot is added to the target region.  
5. Once the replication is completed, you can view the new snapshot in the snapshot list of the target region.
> The source snapshot cannot be deleted during the cross-region replication of this snapshot.
>
 During the process of cross-region replication:
 - Status of source snapshot: you can view it by going to the source region’s [snapshot list](https://console.cloud.tencent.com/cvm/snapshot) and looking in the status column on the source snapshot’s row.
 - Status of target snapshot: you can view it by going to the snapshot list page of the target region.
