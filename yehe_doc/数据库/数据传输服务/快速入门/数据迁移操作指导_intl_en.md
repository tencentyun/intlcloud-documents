
## References
- [Data Migration Overview](https://intl.cloud.tencent.com/document/product/571/13711)
- [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647)

## Overall process
| **Operation Process**              | **Description**                                                     |
| ------------------------- | ------------------------------------------------------------ |
| 1. Prepare               | Before creating a data migration task, you need to prepare the source and target databases and a network environment as instructed in [Overview](https://intl.cloud.tencent.com/document/product/571/42652) to meet the environment requirements. |
| 2. Create a data migration task | This section provides only a basic sample migration task. For more scenarios, see [Migration from MySQL to TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/571/42645). |
| 3. View the task progress or perform other operations | <li>You can view the overall migration progress and details and perform operations such as verification and retry as instructed in [Viewing Task](https://intl.cloud.tencent.com/document/product/571/42637).<li>You can view various data migration metrics as instructed in [Viewing Monitoring Metric](https://intl.cloud.tencent.com/document/product/571/42606).</li> |
| 4. Perform business cutover               | You need to select an appropriate time for business cutover to reduce the impact on the business. For more information, see [Cutover Description](https://intl.cloud.tencent.com/document/product/571/42612). |

## Sample data migration task

1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, and click **Create Migration Task** to enter the **Create Migration Task** page.
2. On the **Create Migration Task** page, select the types, regions, and specifications of the source and target instances and click **Buy Now**.
![](https://qcloudimg.tencent-cloud.cn/raw/1dd520b47977a736e4b7a70e9771ab51.png)
3. On the **Set source and target databases** page, configure the task, source database, and target database settings. After the source and target databases pass the connectivity test, click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/d5c7ca05686e039f5b2074c0d2609597.png)
4. On the **Set migration options and select migration objects** page, configure the migration type and objects and click **Save**.
>? You can select up to 6,000 objects in each migration task.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/497ddacf50988903a25679d48d6b51d2.png" style="zoom:67%;" />
5. On the task verification page, verify the task. After the verification is passed, click **Start Task**.
    If the verification failed, you can view the specific check items and failure reasons, fix the problem as prompted, and initiate the verification task again.
    ![](https://qcloudimg.tencent-cloud.cn/raw/8b12ecee362d8eb7ac583de44961143f.png)
6. Return to the data migration task list, and you can see that the task has entered the **Preparing** status. After 1–2 minutes, the data migration task will be started.
   - Select **Structural migration** or **Full migration**: Once completed, the task will be stopped automatically.
   - Select **Full + Incremental migration**: After full migration is completed, the migration task will automatically enter the incremental data sync stage, which will not stop automatically. You need to click **Complete** to manually stop the incremental data sync.
     - Manually complete incremental data sync and business switchover at appropriate time.
     - Check whether the migration task is in the incremental sync stage without any lag. If so, stop writing data to the source database for a few minutes.
     - Manually complete incremental sync when the data gap between the target and the source databases is 0 MB and the time lag between them is 0 seconds.
   ![](https://qcloudimg.tencent-cloud.cn/raw/676ec6dbceda15c8f74690cde7d23845.png)

