## Overview

[Log cleansing](https://intl.cloud.tencent.com/document/product/436/16920) is a log file processing solution provided by COS based on [SCF](https://www.tencentcloud.com/document/product/583). After it is enabled or you upload log files on your own, the function preconfigured by COS will be automatically triggered to filter, cleanse log content based on the preset SQL search statements, and deliver the result to the specified bucket and path.

## Notes

- Log Cleansing uses the data extraction APIs of COS. For more information on the restrictions, see [SELECT Overview](https://intl.cloud.tencent.com/document/product/436/32472).
- If you have added a log cleansing rule to your bucket in the COS console, a log cleansing function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete or modify this function. Otherwise, your rule may not take effect.
- Currently, Log Cleansing is available only in the Guangzhou, Shanghai, Beijing, and Chengdu regions.
- The Log Cleansing feature depends on the SCF service, which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier according to [SCF pricing](https://intl.cloud.tencent.com/document/product/583/12281).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **App Integration** > **Extended Features** and find **Log Cleansing**.
3. Click **Configure Log Cleansing Rule** to enter the rule configuration page.
4. Click **Add Function**.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
> 
5. In the pop-up window, configure the following items:

	- **Function Name**: Uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
	- **Associated Bucket**: A COS bucket that stores the log files.
	- **Event Type**: An operation that triggers SCF. Take upload as an example. You can initiate an upload by calling the `PUT Object` or `POST Object` API. If you choose **Create using PUT method** as the event type, log cleansing will be triggered only for log files uploaded via the `PUT Object` API.
>! If you intend to upload files to the bucket in multiple ways, such as simple upload, multipart upload, and cross-region replication, we recommend you select **File upload** as the event type.
>
	- **Trigger Condition**: The upload path that will trigger SCF. If you select **Specified Range**, SCF will be triggered only when a log file is uploaded to a path in the specified range. If you choose **The whole bucket**, SCF will be triggered as long as a log file is uploaded to any location of the bucket.
	- **SCF Authorization**: Required. To cleanse a log file, SCF should be authorized to read the log file from your bucket and upload the cleansed log file to the specified location.
6. Click **Next** to configure log cleansing. The configuration items are described as follows:

	- **Source File Configuration**: Includes the file type, column/row delimiter, file header, and compression format configuration for file retrieval.
	**SQL Expression**: You can enter a custom search statement or use the SQL templates provided. For more information on SQL expression, see [SQL Functions](https://intl.cloud.tencent.com/document/product/436/32474).
	- **Output Configuration**: Includes the export format, column/row delimiter, and escape configuration.
7. Click **Next** to configure delivery. The configuration item is as follows:

	- **Destination Bucket**: A bucket that stores the generated file after the log cleansing is completed.
	- **Destination Path**: A path to deliver the log cleansing result. To avoid triggering a loop, we recommend you set it to a path whose prefix is different from that (if any) set in Trigger Condition.
>! If the configured delivery prefix overlaps with that set in the trigger condition, a loop may be triggered. Assume that delivery prefix is set to `prefix/target/` and the prefix set in the trigger condition is `prefix/`. Then, an uploaded log file named `prefix/test.csv` will be cleansed and the result will be delivered to `prefix/target/test.cos_select_result.csv`, triggering a cleansing loop.
> 
8. Click **Confirm**.
You can perform the following operations on the created function:
 - Click **Log** to view the historical running status of log cleansing. If an error is reported, you can click **Log** to quickly redirect to the SCF console to view its details.
 - Click **More** > **Edit** to modify the log cleansing rule.
 - Click **More** > **Delete** to delete the unwanted log cleansing rule.

