## Overview

This document describes how to back up data stored in the cloud. COS provides the following three methods to facilitate backup of data stored in COS:

- Backup and disaster recovery scheme based on cross-region replication
- Batch data replication scheme (COS batch operation feature)
- Migration and backup scheme based on Migration Service Platform (MSP)

## Backup and Disaster Recovery Scheme Based on Cross-region Replication

With the cross-region replication feature, COS can automatically and asynchronously replicate **new objects** added to one bucket to another bucket in a different region. When cross-region replication is enabled, COS will accurately replicate the object content (such as object metadata and version ID) in the source bucket to the destination bucket, and the object copies contain exactly the same attribute information.

For more information, please see [High-Availability Disaster Recovery Architecture Based on Cross-region Replication](https://intl.cloud.tencent.com/document/product/436/32535).

#### Use cases

- **Remote disaster recovery:** COS has 11 nines of availability for object data, but there is still a slight chance of data loss due to force majeure such as wars and natural disasters. If you want to avoid data loss by explicitly having a separate copy in a different region, you can use cross-region replication to achieve remote disaster recovery. In this way, when the IDC in one region is damaged due to force majeure, the IDC in the other region can still provide data copies for your use.
- **Compliance:** COS ensures data availability by providing multiple copies and erasure codes for data in physical disks by default. However, there may be compliance requirements in some industries stipulating that you keep copies in another region. Cross-region replication allows data to be replicated across regions to meet such requirements.
- **Access latency reduction:** when you have end users accessing objects from different regions, with cross-region replication, you can maintain object copies in the available storage regions closest to them, which can minimize access latency to deliver a better user experience.
- **Special technical requirements:** if you have computing clusters in two different regions and the clusters need to process the same set of data, with cross-region replication, you can maintain object copies in both regions.
- **Data migration and backup:** you can copy your business data from one availability region to another one as needed to implement data migration and backup.

#### Usage

For more information, please see [Setting Cross-Region Replication](https://intl.cloud.tencent.com/document/product/436/19235).

## Batch Data Replication Scheme

The COS batch operation feature enables you to perform large-scale batch replication operations at the object level.

#### Use cases

For some business reasons, you may need to back up all data in an existing bucket to another bucket to ensure data availability and reliability.

#### Usage

For more information, please see [Batch Operation](https://intl.cloud.tencent.com/document/product/436/32956).

#### Instructions

The batch replication operation should be used in conjunction with the inventory feature. For more information on inventory, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622). This operation allows you to replicate the specified objects in batches from the source bucket to the destination bucket in the same region or in different regions. It supports customizing parameters for the `PUT Object-copy` operation, and the metadata and storage class of the copy are subject to the configuration information. For more information, please see [PUT Object - copy](https://intl.cloud.tencent.com/document/product/436/10881).

>
> - All objects to be replicated must be in the same bucket.
> - Only one destination bucket can be configured for a batch replication job.
> - You need to have permission to read objects from the source bucket and write objects into the destination bucket.
> - The total size of the objects cannot exceed 5 GB.
> - Verification via ETags and server-side encryption using custom keys are not supported.
> - If the destination bucket does not have versioning enabled and contains an object file with the same name as a file to be replicated, COS will overwrite the object file.

## Data Migration and Backup Scheme

Tencent Cloud Migration Service Platform (MSP) provides easy and fast resource migration schemes. After you create a migration job, you can view the migration progress, migration report, and much more in the MSP Console. For detailed directions, please see [COS Migration](https://intl.cloud.tencent.com/document/product/1036/33184).

