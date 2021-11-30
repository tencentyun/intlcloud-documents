## Overview

COS introduces the [SCF](https://intl.cloud.tencent.com/document/product/583)-based Log Cleansing feature for users to process log files. When you upload a log file or enable [Logging](https://intl.cloud.tencent.com/document/product/436/16920), the cloud function preset by COS will be triggered, which automatically cleanses log messages using the SQL expression you set in the function, and delivers the result to the specified bucket and path.

## Notes

- Log Cleansing uses the data extraction APIs of COS. For more information about the restrictions, please see [SELECT Overview](https://intl.cloud.tencent.com/document/product/436/32472).
- If you have added a log cleansing rule to your bucket in the COS console, a log cleansing function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete or modify this function. Otherwise, your rule may not take effect.
- Currently, Log Cleansing is available only in the Guangzhou, Shanghai, Beijing, and Chengdu regions.
- The Log Cleansing feature depends on the SCF service, which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier according to [SCF Product Pricing](https://intl.cloud.tencent.com/document/product/583/12281).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Application Integration**. Then, select the **Data Processing** tab and find **Log Cleansing**.
3. Click **Configure Backup Rule** to go to the rule configuration page.
4. Click **Add Function**.
> !If you haven’t activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.

5. In the pop-up window, configure the following information:

	
	- **Function Name**: uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
	- **Associated Bucket**: a COS bucket that stores the log files.
	- **Event Type**: an operation that triggers SCF. Take upload as an example. You can initiate an upload by calling the `PUT Object` or `POST Object` API. If you choose **Create using PUT method** as the event type, log cleansing will only be triggered by a log file uploaded via the `PUT Object` API.
>!If you intend to upload files to the bucket using multiple ways, such as simple upload, multipart upload, and cross-bucket replication, you are advised to choose **File upload** as the event type.
	- **Trigger Condition**: the upload path that will trigger SCF. If you select **Specified Range**, SCF will be triggered only when a log file is uploaded to a path in the specified range. If you choose **The whole bucket**, SCF will be triggered as long as a log file is uploaded to any location of the bucket.
	- **SCF Authorization**: Required. To cleanse a log file, SCF should be authorized to read the log file from your bucket and upload the cleansed log file to the specified location.

6. Click **Next** to configure log cleansing. The configuration items are described as follows:

	- **Source File Configuration**: includes the file type, column/row delimiter, file header, and compression format configuration for file retrieval.
		- **SQL Expression**: You can enter a custom search statement or use the SQL templates provided. For more information about SQL expression, please see [SQL Functions](https://intl.cloud.tencent.com/document/product/436/32474).
	- **Output Configuration**: includes the export format, column/row delimiter, and escape configuration.

7. Click **Next** to configure delivery. The configuration items are described as follows:


	- **Destination Bucket**: a bucket that stores the generated file after the log cleansing is completed.
	- **Destination Path**: a path to deliver the log cleansing result. To avoid triggering a loop, you are advised to set it to a path whose prefix is different from that (if any) set in Trigger Condition.
> !If the configured Delivery Prefix overlaps with that set in Trigger Condition, a loop may be triggered. Assume that Delivery Prefix is set to `prefix/target/` and the prefix set in Trigger Condition is `prefix/`. Then, an uploaded log file named `prefix/test.csv` will be cleansed and the result will be delivered to `prefix/target/test.cos_select_result.csv`, triggering a cleansing loop.

8. Click **Confirm**.

     You can perform the following operations on the created function:
   - Click **View Log** to view the historical running status of the log cleansing. If an error is reported, you can click **View Log** to quickly redirect to the SCF console for viewing the error log details.
   - Click **Edit** to modify the log cleansing rule.
   - Click **Delete** to delete an unwanted log cleansing rule.

