## Overview

The COS console features a Dashboard where you can have an overview of your storage data, including the number of buckets, number of objects, storage usage, request counts, and traffic.

> - To view the above data using a sub-account, you need to have the **bucket list access** permission. For more information, see “Adding a Preset Policy” in [Accessing Bucket List Using Sub-Account](https://intl.cloud.tencent.com/document/product/436/17061).
> - Only **Number of Buckets** is a real-time metric on this dashboard, while the other metrics are delayed by approximately 2 hours. All of these metrics are for monitoring purposes only. For detailed billing data, please go to the [Billing Center](https://console.cloud.tencent.com/account).

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), and click **Monitoring Management** > **Dashboard** to open the data overview page.
2. In the **Dashboard** window, you can view the following:
   ![](https://main.qcloudimg.com/raw/036d7c5f1e31fa9f69507733c2a4d8d9.png)
	- **Number of Buckets**: the total number of objects that have been created across all your buckets. You can view this data for different storage classes.          
	- **Number of Objects**: the total number of objects that have been created across all buckets.                      
	- **Daily Average XXX Storage of This Month**: the average daily storage usage for this month, as measured in current storage usage/days of this month. This metric is displayed by storage class:  STANDARD, STANDARD_IA, and ARCHIVE.
	- **Storage**: shows your storage usage details for STANDARD, STANDARD_IA, and ARCHIVE for the month to date or the last 30 days.
	- **Traffic**: shows your traffic details for the month to date or the last 30 days, currently covering public network downstream traffic, private network traffic, and CDN origin-pull traffic in STANDARD and STANDARD_IA storage classes.
	- **Request Counts**: shows the number of your read/write requests to the STANDARD and STANDARD_IA storage classes for the month to date or the last 30 days. 
	- **Success Rate of User Requests**: shows the success rate of your read/write requests to the STANDARD storage class for the month to date or the last 30 days. 
	- **Data Retrieval**: shows your data retrievals for STANDARD_IA and ARCHIVE for the month to date or the last 30 days. For ARCHIVE storage class, it covers Expedited Retrieval, Standard Retrieval, and Bulk Retrieval.
	- **Bucket Overview**: shows the key metrics for each bucket under Yesterday or This Month. These metrics may vary depending on the storage class you choose, including storage usage for STANDARD, STANDARD_IA, and ARCHIVE, data retrievals for STANDARD_IA and ARCHIVE, read/write requests to STANDARD and STANDARD_IA, public network downstream traffic, private network downstream traffic, and CDN origin-pull traffic.
3. You can export the **Bucket Overview** list by clicking the download icon on the upper right corner. 
