## Overview

The data migration service is an online concurrent migration service provided by CFS to migrate massive amounts of data. It allows you to easily migrate data from sources such as Tencent Cloud and other mainstream object storage systems to CFS for efficient data transfer.

## Use Cases

### Data loading

In machine learning and autonomous driving scenarios, certain datasets are originally put in object storage. When frequent access is required for training and inference, data can be quickly loaded to High-Performance CFS through the migration service for more efficient data reads.

### Cross-cloud data migration

Object storage can be directly accessed over the public network, which means file data from other clouds can be transferred to object storage and then to CFS through the data migration service.

### Cross-account data migration

When CFS data is migrated from one account to another, the cross-account access capabilities of object storage can be used to implement cross-account data migration.

## Strengths

- Supports data migration from mainstream cloud services.
 - Supports migrating COS data to CFS, where all download traffic is over Tencent Cloud's private network, without incurring traffic fees. 
 - Supports migrating data from mainstream object storage services to CFS.
- Various data migration methods.
 - Bucket migration: Migrates all data according to the specified bucket path.
 - Inventory migration: Filters objects by time period and file prefix (specified directory) based on the object storage inventory list for finer-grained migration.
 - Supports overwriting by last modified time, full overwriting, and no overwriting.
- Flexible overwriting methods.
Inventory migration: Filters objects by time period and file prefix (specified directory) based on the object storage inventory list for finer-grained migration.
- More secure and efficient data transfer methods
 - Migration monitoring: Provides the real-time information of the running status, traffic, and progress of migration tasks.
 - Migration details: Provides detailed migration information such as the number of files, file size, file list, and status.
 - Automatic retry: Three automatic retries are performed in the case of various temporary errors to enhance the migration efficiency.




