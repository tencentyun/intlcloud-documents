## Overview
This feature allows you to perform an overall analysis of HDFS storage, including the total number of files, total storage usage, file distribution, and recent trends in file storage as of the day before the current day (T-1). It also provides top directory lists for large and small files.
- You can view the daily changes and recent trends in the total number of files and total storage usage based on HDFS storage within a cluster.
- The file count and storage usage pie charts can help you understand the proportion of small files and the storage used by them.
- The feature also allows you to query and download directory information for the top 1,000 large/small files as of the last collection time.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the corresponding cluster in the cluster list.
2. On the cluster details page, click **Cluster Service** and choose **Operation** > **File Storage Analysis** in the top-right corner of the HDFS component block to view information about relevant files stored on **HDFS** and their directories as of the last collection time.
3. Obtain statistical views.
<ol>
<li>You can view the daily increase and day-over-day change in the total number of files stored on HDFS and total storage usage.</li>
<li>Pie charts are provided to show you the numbers of empty files (size = 0 MB), small files (size ≤ 2 MB), other files (2 MB < size < 128 MB), and large files (size ≥ 128 MB), and the storage used by each of the four categories of files.<br></li>
</ol>
4. You can view recent trends in the number and storage usage of different categories of files.
5. You can query and download information about the top 1,000 small/large files as of the day before the current day (T-1), including the file name, file path, file size, user group, owner, and last access time.

<dx-alert infotype="alarm" title="Risk description">
The data required for file storage analysis is collected at 14:00 (Beijing time) every day.
1. The file storage analysis involves collecting and analyzing backup FsImage files, which can increase the memory usage of the local machine (a maximum increase of 4 GB). If the proportion of machines in the cluster that are using memory consistently remains at a high level, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to disable the feature. 
2.. In HA clusters, the analysis feature is executed on the Standby Master node, while in non-HA clusters, the feature is executed on the Master node.
</dx-alert>



