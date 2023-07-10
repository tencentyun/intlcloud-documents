## Overview

You can go to the **Statistic** page in the COS console to view the number of buckets/objects/requests, storage usage, traffic, and other data.

>!
> - If a sub-account needs to view the statistics, it needs to have permission to **access the bucket list**. For more information, see **Adding a Preset Policy** in [Accessing Bucket List Using Sub-Account](https://www.tencentcloud.com/document/product/436/17061).
> - Except for the **number of buckets**, other data is not real-time and has a delay of about 2 hours. The data is for monitoring purposes only. To view the accurate billing data, go to [Billing Center](https://console.cloud.tencent.com/account).
> 

## Viewing Line Charts

### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Statistic** > **Basic Statistic** on the left sidebar.
2. On the **Basic Statistic** page, you can view the following information:
   ![](https://qcloudimg.tencent-cloud.cn/raw/7cdb582b1cbb4859ffce7cf69d23b212.png)
    - **Number of Buckets**: number of buckets that have been created                                     
    - **Total Objects**: number of objects that have been created in all buckets. You can view the number of objects by storage class.                      
    - **Average Daily Usage for This Month**: The average daily usage by storage class (i.e., STANDARD, MAZ_STANDARD, STANDARD_IA, MAZ_STANDARD_IA, INTELLIGENT TIERING, MAZ_INTELLIGENT TIERING, ARCHIVE, and DEEP ARCHIVE). Daily storage usage = sum of the "5-minute usage"/288 (number of statistical points). Average daily storage usage for this month = sum of the daily storage usage in this month/number of days in this month.
   - **Storage Usage**: Storage usage for STANDARD, MAZ_STANDARD, STANDARD_IA, MAZ_STANDARD_IA, INTELLIGENT TIERING, MAZ_INTELLIGENT TIERING, ARCHIVE, and DEEP ARCHIVE. You can view the data for the past 93 days, and the time range for each query cannot exceed 31 days.
   - **Traffic**: Public/private downstream traffic and CDN origin-pull traffic for STANDARD, MAZ_STANDARD, STANDARD_IA, MAZ_STANDARD_IA, INTELLIGENT TIERING, and MAZ_INTELLIGENT TIERING. You can view the data for the past 93 days, and the time range for each query cannot exceed 31 days.
   - **Request Count**: Number of read/write requests for STANDARD, MAZ_STANDARD, STANDARD_IA, MAZ_STANDARD_IA, INTELLIGENT TIERING, and MAZ_INTELLIGENT TIERING. You can view the data for the past 93 days, and the time range for each query cannot exceed 31 days.
   - **Request Success Rate**: Request success rate for STANDARD and MAZ_STANDARD. You can view the data for the past 93 days, and the time range for each query cannot exceed 31 days.
   - **Data Retrieval**: The amount of data retrieved for STANDARD_IA, MAZ_STANDARD_IA, INTELLIGENT TIERING, MAZ_INTELLIGENT TIERING, ARCHIVE, and DEEP ARCHIVE. For ARCHIVE, the amount is classified into expedited retrievals, standard retrievals, and bulk retrievals. You can view the data for the past 93 days, and the time range for each query cannot exceed 31 days.
3. You can click the download button in the upper-right corner of each chart to download the data. 

## Viewing Bucket-Level Data

### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left sidebar, and click **Statistical Data**.
2. On the **Statistical Data** page,  you can view the bucket data such as storage usage, data retrievals, traffic, and request count within a specified period of time.

