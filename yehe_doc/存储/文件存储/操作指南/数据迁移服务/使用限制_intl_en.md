
| Limit | Description |
|---------|---------|
| Migration source | Data can be migrated only from object storage, including mainstream object storage sources in the Chinese mainland. |
| Migration destination | Data can be migrated only to CFS, which can be Standard (NFS), High-Performance (NFS), Standard Turbo, or High-Performance Turbo. |
| Progress display | Currently, the migration progress is updated once for every 1,000 files. If fewer than 1,000 files are migrated, the progress may deviate to some extent. |


## Notes

- The data migration service is free of charge. If data migration crosses regions or clouds, the outbound traffic of the source object storage will be charged. No outbound traffic fees will be incurred only when data is migrated from COS to CFS in the same region.
- If the source data is large in volume, you can use bucket migration or inventory migration. Specifically, use different bucket directories and inventories for different tasks to accelerate the migration. We recommend you run up to three tasks. Do not start multiple identical tasks for the same batch of data, which will lead to unnecessary metadata verification and prevent acceleration.
