## Overview

If COS log storage is enabled, you can use the log analysis feature to further analyze the generated log files. This feature consolidates log files within a specified time range for statistical analysis and extracts key metrics for your reference.

## Prerequisites

To use the log analysis feature, you need to [Enable COS Log Storage](https://intl.cloud.tencent.com/document/product/436/17040), and then create a log analysis function. For detailed instructions, see [Adding Log Analysis Function](https://intl.cloud.tencent.com/document/product/436/45569).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Choose **Bucket List** on the left sidebar.
3. Click the bucket that requires log analysis.
4. On the left sidebar, select **Log Management** > **Logging**.
>! To use the log analysis feature, first enable log storage as instructed in [Setting Logging](https://intl.cloud.tencent.com/document/product/436/17040).
>
5. If you have added a COS log analysis function, click **Use Now** in the **COS Log Analysis** section. The system will check whether you have added log analysis function rules.
If you haven’t added such a function, add one as instructed in [Adding Log Analysis Function](https://intl.cloud.tencent.com/document/product/436/45569).
6. Select a corresponding function and time range. Click **New Analysis Task** and configure the following information in the pop-up window: 

 - **Time Range**: Period of logs you want to analyze, up to 30 days. Logs are retrieved according to **end time**. Logs in the specified time range cannot exceed 200 GB.
 - **Cloud Function**: Select a COS log analysis function added in the region where this bucket resides.
 - **Product Destination Directory**: After analysis, the output result will be zipped and saved to the directory you set. The output file contains **result file** and **inventory file**. **Result file** is based on the scenario you select. **Inventory file** refers to the log file list retrieved for this analysis.
 - **Scenario**: Scenario supported by this analysis.
 - **Value of N**: It must be a positive integer.
 - **Task Description**: Custom description.
7. Click **Confirm**.

   You can perform the following operations on the created task:
 - Click **View Result** to view the result of this analysis task and where the result files are saved.
>! 
>- You can query log analysis tasks created in the last 3 days.
>- You can view the result only after a log analysis task is finished. A task takes a few to tens of minutes depending on the log size.
 - Click **Running Log** to go to the SCF console and view logs of COS log analysis.
