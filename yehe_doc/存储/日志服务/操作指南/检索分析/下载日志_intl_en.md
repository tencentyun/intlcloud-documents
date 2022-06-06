## Overview
CLS allows you to export the collected log data, so you can download the data to view it locally.
The log download feature is as described below:
- Up to 50 million logs can be downloaded at a time.
- Search conditions and search time range can be specified.
- JSON and CSV export formats are supported.

>? Only raw logs can be downloaded. To download statistical analysis results (SQL execution results), click <img src="https://main.qcloudimg.com/raw/53b7030f85123fe5658e7cce23b730c8.png"></img> in the upper-right corner.
>

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Search and Analysis** to go to the search and analysis management page.
3. Click the drop-down lists of **Logset** and **Log Topic** to select the content to be searched.
![](https://qcloudimg.tencent-cloud.cn/raw/8594f9cc1e8780f5ec0645deac120b51.png)
4. Click **Log Time** and select a log time for search.
You can select **Recent Time** or **Relative Time** or customize the time range.
5. Click **Search and Analysis**.
6. After the log data is returned, click <img src="https://main.qcloudimg.com/raw/53b7030f85123fe5658e7cce23b730c8.png"></img> to **download logs**.
![](https://qcloudimg.tencent-cloud.cn/raw/f5af6beb79610ca69c488f44f6f655db.png)
>? If no log data is returned, you cannot download logs.


7. In the pop-up window, confirm the time range of the logs to be downloaded and the search statement and download log data according to the following settings:

<ul>
	<li>Data format: "CSV format" or "JSON format" can be selected as needed.</li>
	<li>Log sorting: logs can be sorted in "ascending" or "descending" (default) order by time.</li>
	<li>Log quantity: "All logs" are exported by default. You can also select a "custom log quantity".</li>
</ul>

>? 
> - For the CSV format, only fields with configured indexes can be exported, and the downloaded logs may be empty.
> - For the JSON format, all fields can be exported, regardless of index configuration.
> - If the number of logs to be downloaded exceeds 50 million, you are advised to narrow the search scope (for example, use more precise search conditions or narrow the search time range) or download only a specified number of logs.
> - If you do need to download more than 50 million logs, you can set the log search time range to create multiple download tasks and download logs in batches.


8. Click **Export** to switch to the **Export Logs** page.

>? A download task can be in any of the following states: **Waiting**, **File generating**, and **File generated**. A newly created download task waits for a while before entering the **File generating** state and starts generating data files in the background. If multiple download tasks are created at the same time, the system executes them in sequence based on the creation time. Tasks that are created later are in the **Waiting** state.

9. After the **File Name/Task ID** status changes to **File generated successfully**, click **Download** to export the logs.
>! The exported log file is retained for only 3 days.
> 
