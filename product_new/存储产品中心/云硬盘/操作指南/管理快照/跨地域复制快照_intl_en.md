Cloud disk snapshots currently support cross-region snapshot replication. This feature allows you to easily migrate data and services to other regions, or build a cross-region disaster recovery system for your business.
Cross-region snapshot replication is currently in beta test. You can **submit an application**.

## Use Limits
**Whitelisted users only**: Cross-region snapshot replication is currently in beta test. You need to **submit an application** to use this feature.
- **Supported Regions**: This feature is currently available in Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Bombay, and Guangzhou Open. We will provide this feature to all regions soon.
- **Snapshot Rollback**: New snapshot created via cross-region snapshot replication is not associated with the source disk. Therefore, the rollback feature is not available for the newly replicated snapshot.

## Steps
1. Access the **Snapshot List** page.
2. Click **Cross-Region Replication** for the target snapshot.
3. Configure the following parameters:
  - New snapshot name: Enter the new snapshot name, which is a string of up to 60 characters (optional).
    By default, a new snapshot name contains the source snapshot ID and region information, with the following format: `Copied <Source snapshot ID> from <Source snapshot region>`, for example, `Copied snap-oi5spwt2 from ap-shanghai`.
  - Region: Select the destination region (required).
    Please check the snapshot quota and region restriction when you select the region.

4. Click **Confirm** to start the replication. The status of the source snapshot will be displayed, and the new snapshot will be added to the destination region. Once the replication is completed, you can view the new snapshot in the snapshot list of the destination region.
> The source snapshot cannot be deleted during the cross-region replication of this snapshot.
>
