### Will the data in the source database be deleted after migration with DTS?
No. Data migration with DTS essentially replicates the data from the source database to the target database, without affecting such data.

### How does data migration with DTS affect the target database?
When data is migrated to the target database, the system will verify whether the source and target databases have tables with the same name, and if so, the verification will fail, and you will be prompted to make changes first.

### Does DTS support migration from one offline database to another?
No. DTS only supports migration from self-built databases, databases in other clouds, or TencentDB databases to TencentDB databases.

### Does DTS support data migration between TencentDB instances under two different Tencent Cloud accounts?
Yes. For migration between TencentDB instances under two different Tencent Cloud accounts, you need to log in to DTS with the Tencent Cloud account of the target instance. For detailed directions, see [Cross-account TencentDB Instance Migration](https://intl.cloud.tencent.com/document/product/571/42646).

### Can I configure multiple DTS tasks for migration from the same source database to different TencentDB instances?
Yes. You can migrate data from the same source database to multiple target databases and vice versa, but multiple concurrent tasks may increase the access pressure on the source and target databases and thus slow down the migration. If you need to create multiple migration tasks for the same source database, then after creating the first task, you can quickly create similar tasks by clicking **More** > **Create similar task** in the **Operation** column.

### Does DTS support scheduled automatic migration?
Yes. When modifying the configuration for a created data migration task, you can select scheduled migration and specify the start time.

### Can I monitor the task progress during migration?
Yes. You can log in to the [DTS console](https://console.cloud.tencent.com/dtsnew/migrate/page) and view the migration task progress on the **Data Migration** page.

### Why is there a 15-day limit on incremental migration?
Currently, incremental migration is performed through the nearest proxy server via Tencent Cloud Direct Connect, which eliminates network jitters and ensures the quality of data transfer. The 15-day limit can reduce the connection pressure on the proxy server and is only intended for reasonable utilization of resources for migration. Connections will not be force closed after 15 days.

### How is the data accuracy ensured during data migration?
DTS uses Tencent Cloud's proprietary data migration architecture to verify the data accuracy in real time and quickly detect and correct errors. This guarantees the reliability of the transferred data.

### Why does data verification require that the source database instance not be read-only?
This is because data verification requires creating a new database `__tencentdb__` in the source instance and writing the checksum table to the database. If the instance is read-only, data verification will be skipped.

### Can I specify tables for migration with DTS?
Yes. You can select the entire instance or specify tables as the migration object.

### When does data migration stop?
When you select incremental migration, if it takes a long time before the task stops, you may need to stop it by yourself.
- If you select **Structural migration** or **Full migration** as the **Migration Type**, the task will automatically stop upon completion.
- If you select **Full + Incremental migration** as the **Migration Type**, after full migration is completed, the migration task will automatically enter the incremental data sync stage, which will not stop automatically. You need to click **Done** to manually stop the incremental data sync.
  - Manually complete incremental data sync and business switchover at appropriate time.
  - Check whether the migration task is in the incremental sync stage without any lag. If so, stop writing data to the source database for a few minutes.
  - Manually complete incremental sync when the data gap between the target and the source databases is 0 MB and the time lag between them is 0 seconds.

### Why does the data size change before and after full migration?
This is because the fragmented spaces of the source and target databases are different, and the source database may contain data holes. In this case, after full migration is completed, the table storage space in the target database may be smaller than that in the source database. We recommend you perform a data consistency check as instructed in [Creating Data Consistency Check Task](https://intl.cloud.tencent.com/document/product/571/42724) after the migration is completed to check whether the contents of the source database and the target database are consistent.

### Is double write supported during data migration?
No. Writing data to both the source and target databases during migration may cause data inconsistency.

### Does DTS support cross-region database migration?
Yes. You can implement cross-region data transfer over the public network.

### What Redis versions does DTS support migrating?
The target database version must be later than or equal to the source database version. Supported source and target versions are as follows: 

| Source                                                          | Target                                 |
| ------------------------------------------------------------ | -------------------------------------- |
| Self-built database (including CVM-based ones) on Redis 2.8, 3.0, 3.2, 4.0, or 5.0 | TencentDB for Redis 2.8, 3.0, 3.2, 4.0, or 5.0 |
| TencentDB for Redis 2.8, 3.0, 3.2, 4.0, or 5.0                       | TencentDB for Redis 2.8, 3.0, 3.2, 4.0, or 5.0 |
| Databases in other clouds on Redis 2.8, 3.0, 3.2, 4.0, or 5.0                   | TencentDB for Redis 2.8, 3.0, 3.2, 4.0, or 5.0 |

### Can I create multiple DTS tasks for migration from the same source database to different TencentDB instances?
Yes. You can migrate data from the same source database to multiple target databases and vice versa, but multiple concurrent tasks may increase the access pressure on the source and target databases and thus slow down the migration. If you need to create multiple migration tasks for the same source database, then after creating the first task, you can quickly create similar tasks by clicking **Create similar task** in the **Operation** column.

