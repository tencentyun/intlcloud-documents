## Overview

You can go to the **Statistic** page in the COS console to view the number of buckets/objects/requests, storage usage, traffic, and other data.

>!
> - If a sub-account needs to view the statistics, it needs to have permission to **access the bucket list**. For more information, please see **Adding a Preset Policy** in [Accessing Bucket List Using Sub-Account](https://intl.cloud.tencent.com/document/product/436/17061).
> - Except for the **number of buckets**, other data is not real-time and has a delay of about 2 hours. The data is for monitoring purposes only. To view the accurate billing data, go to [Billing Center](https://console.cloud.tencent.com/account).
> 

## Viewing Line Charts

### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Statistic** > **Basic Statistic** on the left sidebar.
2. On the **Basic Statistic** page, you can view the following information:
   ![](https://qcloudimg.tencent-cloud.cn/raw/7cdb582b1cbb4859ffce7cf69d23b212.png)
   - **Number of Buckets**: Number of buckets that have been created                                     
    - **Total Objects**: Number of objects that have been created in all buckets. You can view the number of objects by storage class.                      
    - **Average Daily Usage for This Month**: The calculation formula is as follows: Current storage usage/Number of days in the month. You can view the average daily usage for this month by storage class (e.g., STANDARD, MAZ_STANDARD, STANDARD_IA, MAZ_STANDARD_IA, and ARCHIVE).
   - **Storage Usage**: Storage usage for STANDARD, MAZ_STANDARD, STANDARD_IA, and ARCHIVE. You can view the data for the past year.
   - **Traffic**: Public/private downstream traffic and CDN origin-pull traffic for STANDARD, MAZ_STANDARD, and STANDARD_IA. You can view the data for the past year.
   - **Request Count**: Number of read/write requests for STANDARD, MAZ_STANDARD, and STANDARD_IA. You can view the data for the past year. 
   - **Request Success Rate**: Request success rate for STANDARD and MAZ_STANDARD. You can view the data for the past year. 
   - **Data Retrieval**: The amount of data retrieved for STANDARD_IA and ARCHIVE. For ARCHIVE, the amount is classified into expedited retrievals, standard retrievals, and bulk retrievals. You can view the data for the past year.
   - **Bucket Overview**: Displays metrics of yesterday or this month for each bucket. The metrics displayed vary depending on the storage class selected, and include STANDARD/MAZ_STANDARD/STANDARD_IA/ARCHIVE storage usage, STANDARD_IA/ARCHIVE data retrievals, STANDARD/MAZ_STANDARD/STANDARD_IA read/write requests, public/private downstream traffic, and CDN origin-pull traffic.
3. You can click the download button in the upper-right corner of each chart to download the data. 

## Viewing Bucket-Level Data

### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left sidebar, and click **Statistical Data**.
2. On the **Statistical Data** page,  you can view the bucket data such as storage usage, data retrievals, traffic, and request count within a specified period of time.
