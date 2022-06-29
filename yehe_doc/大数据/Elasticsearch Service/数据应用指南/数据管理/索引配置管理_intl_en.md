## Overview
The data management feature allows you to view and manage indices. You can view the configuration of an index or modify the index configuration on the **Configuration management** page to quickly adapt to business changes.

## Directions
1. Log in to the [ES console](https://console.cloud.tencent.com/es).
2. Select the target cluster in **Data Management**, click **More** in the index list, and select **Configuration management** in the drop-down list to enter the index configuration management page.

### View mode
After entering this page, the view mode is selected by default, where the information of data source configuration, lifecycle configuration, and advanced settings is displayed. You can click **Change to JSON mode** in the top-right corner to view the current index configuration in JSON format.
![](https://qcloudimg.tencent-cloud.cn/raw/c5dbec52fac1c97d73bfb736a1914580.png)
![](https://qcloudimg.tencent-cloud.cn/raw/cf7b5c81959bcd2a22b86a2005547d30.png)


### UI edit mode
In the view mode, click **Modify Configuration** in the bottom-left corner to enter the edit mode, where you can modify the information of the index configuration. After successful modification, lifecycle configurations will apply to all backing indices, and configurations of other items such as shard number, replica shards, and field mappings will take effect only in those rolled over later and will not update existing ones.
>! The time field and write mode cannot be modified.

![](https://qcloudimg.tencent-cloud.cn/raw/2db5eb217eb693e0d57a9cb5d2eb2959.png)

### JSON mode
After switching to the JSON edit mode, the left side is the current configuration of the running index, and the right side is the **Modify Configuration** input box where you can enter the modified configuration information. Corresponding index configuration items will be updated after the modification is saved successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/7c23bbc414ec68c0150501c1e77e4347.png)

As shown in the figure, you can change the storage time before data is moved to the warm tier from 2 hours to 2 days. Click **Confirm**, and the configuration will be updated.
![](https://qcloudimg.tencent-cloud.cn/raw/9b93bbea3cea605aab7e103a003a68d3.png)
