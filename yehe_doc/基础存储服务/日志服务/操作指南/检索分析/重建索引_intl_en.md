## Overview
As an edited index rule takes effect only for logs written after the rule is edited, if you want to reindex historical data according to the latest index rule, you need to use the reindexing feature. Below are common reindexing scenarios:
- A field is added to a key-value index, and historical data needs to be searched for by this field.
- The delimiter configuration is adjusted, and historical data needs to be searched for by the new delimiter.
- Statistics collection wasn't enabled for a field. After it is enabled in the index configuration, the statistics of this field in historical data needs to be collected (i.e., SQL).

During reindexing, the index of raw logs in the specified time range will be rebuilt, which will incur index traffic fees (write traffic fees and index storage fees won't be incurred). If the data volume is high, reindexing will be time-consuming and incur high fees. We recommend you avoid frequently modifying the index configuration and reindexing as much as possible.


## Prerequisites

The index has been enabled, and the latest index configuration can meet future requirements for search and analysis.


## Notes

- Only one reindexing task can be executed for a single log topic at any time, and each log topic can have up to ten reindexing task records. If there are already ten records, you can create a new reindexing task only after deleting an unwanted record.
- Logs for the same time range can be reindexed only once. You need to delete historical task records to reindex such logs again.
- After a reindexing task record is deleted, the index data before reindexing will be restored.
- You can only reindex logs for the time range with a write traffic below 500 MB in the console. If the limit is exceeded, we recommend you narrow down the time range or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase the limit.
- The reindexing time range uses the log time. If the difference between the log upload time and the time range of logs to be reindexed is greater than one hour (for example, a log generated at 2:00 AM is uploaded at 4:00 PM, and logs between 12:00 AM and 12:00 PM need to be reindexed), the log won't be reindexed and cannot be searched for subsequently. If a new log is reported within the time range for which logs have been reindexed, it won't be reindexed and cannot be searched for subsequently either. 




## Directions
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Log Topic** to enter the log topic list page.
3. Click the target log topic ID/name to enter the log topic management page.
4. Select the **Index Configuration** tab and click **Reindex** at the bottom.

5. Select the time range of logs to be reindexed and click **Start Reindexing**.

>? Here, the write traffic and time of the log data to be reindexed is estimated according to the selected time range. If the write traffic is too high and the time is too long, we recommend you narrow down the time range accordingly.
>

6. After reindexing is completed, you can view the completed task in the list. You can also delete the specified task. Once a task is deleted, the index data before reindexing will be restored.


