

This document focuses on how to split/merge topic partitions in the CLS console.


## Splitting a Topic Partition

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and click **Logset** in the left sidebar to enter the logset list page.

2. Locate the logset for which you want to split a log partition, and click on the logset name to enter the log topic list page.

   ![](https://main.qcloudimg.com/raw/8f23b92fbe45348e256edf3e6245bb9e.png)

3. Click on a log topic name to open the Basic Info page. In the **Topic Partition Management** section, select the target topic partition to be split, and click **Edit** to split it.

   ![](https://main.qcloudimg.com/raw/649adde1285a37414ddf34ecd1d3ea46.png)

4. Select Split for **Operation**, enter the split location, which defaults to the median value in the partition range, and then click **OK**.

   ![](https://main.qcloudimg.com/raw/2c2dca3e3fd2e81dcb5e7e448ac4aa3a.png)

5. Once split successfully, the old partition will be read-only (allows no data write or operation), and the two new partitions will allow both read and write access.

   ![](https://main.qcloudimg.com/raw/6aaf256d6de0b5a59b3ce7d11b4c3e14.png)




## Merging Partitions

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and click **Logset** in the left sidebar to enter the logset list page.

2. Locate the logset for which you want to split a log partition, and click on the logset name to enter the log topic list page.

3. Click on a log topic name to open the Basic Info page. In the **Topic Partition Management** section, select the target topic partition to be merged, and click **Edit**.

   ![](https://main.qcloudimg.com/raw/649adde1285a37414ddf34ecd1d3ea46.png)

4. Select **Merge**, and determine the left or right neighboring partition to merge with.

   ![](https://main.qcloudimg.com/raw/93e32728b70eadf9fd0ad452765059d2.png)

5. Once merged successfully, the old partitions will be read-only (allows no data write or operation), and the new partition will allow both read and write access.

![](https://main.qcloudimg.com/raw/6aaf256d6de0b5a59b3ce7d11b4c3e14.png)