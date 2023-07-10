Cross-region snapshot replication is now in beta. With this feature, you can easily migrate data and services to other regions, or build a cross-region disaster recovery system for your business.
Cross-region snapshot replication is now in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.

## Use Limits
- **Application for beta test eligibility**: Cross-region snapshot replication is now in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
- **Supported regions**: For more information, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/362/32396).
- **Finance zones**: Finance zones support replication between finance zones only.
- System disk snapshots are not supported.


## Directions

1. Log in to the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page.
2. Click **Cross-region replication** for the target snapshot.
3. Configure the following parameters:
    - **New snapshot name**: (optional) enter the new snapshot name with up to 60 characters.
    By default, a new snapshot name contains the source snapshot ID and region information in the format of `Copied <Source snapshot ID> from <Source snapshot region>`, such as `Copied snap-oi5spwt2 from ap-shanghai`.
    - **Region**: (required) a target region to which a snapshot is copied
    Check the snapshot quota and geographical restriction when you select the region.
4. Click **OK** to start the replication. Hover over the information icon to view the status of the source snapshot. The new snapshot is added to the target region. 
5. Once the replication is completed, you can view the new snapshot in the snapshot list of the target region.
<dx-alert infotype="notice" title="">
The source snapshot cannot be deleted during the cross-region replication of the snapshot.
</dx-alert>

During the process of cross-region replication:
 - Status of source snapshot: You can view it by going to the source region's [snapshot list](https://console.cloud.tencent.com/cvm/snapshot) and looking in the status column on the source snapshot's row.
 - Status of target snapshot: You can view it by going to the snapshot list page of the target region.

