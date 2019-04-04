## Introduction
CLS can ship logs to Cloud Object Storage (COS) for long-term log data storage. By making configuration in the console, logs can be shipped to COS according to preset shipping intervals, file sizes, paths and filtering rules.

## Directions
### Prerequisites

1. Activate the CLS, create a logset and a log topic, and the log data can be successfully collected.
2. Activate Tencent Cloud COS, and create a bucket in the region of the logset to which shipping tasks belong.
3. Make sure that the current account has the permission to configure shipping. For more information on shipping permissions of a sub-account/collaborator, see [Configuring Shipping Permissions for Sub-Account](https://cloud.tencent.com/document/product/614/33098).

### Procedure
1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Logset** in the left navigation pane.
3. Select the logset to which a shipping task needs to be added, click the logset ID/name to go to its details page.
![](https://main.qcloudimg.com/raw/b4560b57c179e20441fa56bd65803971.png)
4. Locate the log topic to be shipped, click **Configure** -> **Shipping to COS Configuration** to go to the "Shipping Configuration" page.
![](https://main.qcloudimg.com/raw/df645d270b696a380253435e079a8949.png)
5. Click **Add Shipping Task** to go to the **Ship to COS** page to complete the configuration information, and then click **Next**. For more information, see [Configuration Items](#config).
![](https://main.qcloudimg.com/raw/c588bcb6e91bb9849003532968edac44.png)
6. Go to **Advanced Configuration** and select the shipping format, whether to enable compressed delivery, compression format, and shipping filter.
If you select json, you need to make the following configurations:
![](https://main.qcloudimg.com/raw/3711401cfd70d3f583bb82dae1970331.png)
If you select csv, you need to specify the key, separator, escape character, invalid field content, whether to write the key into the first line, etc.
![](https://main.qcloudimg.com/raw/a83f64cd3434e7fd894249e4dea0eb10.png)
 - Key: The key field written to the csv file.
 - Separator: Separators between the fields in the csv file.
 - Escape Character: If the value fields contain the selected separator characters, the separators will be enclosed by escape characters.
 - Invalid Field Filling: If the configured CSV key-value field is an invalid key, the invalid field will be filled.
 - Key in First Line: Write the keys into the first line of CSV file (disabled by default).
7. Check if the shipping status is enabled.
![](https://main.qcloudimg.com/raw/14e70eec382e5dab3803a71752ffd62c.png)

<a id="config"></a>
### Configuration items
#### (Optional) Directory prefix
CLS allows you to define a directory prefix. Log files are shipped to the directory of the COS bucket. Log files are stored under the bucket by default with the path `{COS bucket}{directory prefix}{partition format}_{random}_{index}.{type}`, where `{random}_{index}` is a random number.

#### (Required) Partition format
A directory is generated automatically for the creation times of shipping tasks based on strftime syntax. `/` represents the first level of COS directory. The following is an example where a task is shipped to the bucket "bucket_test/" with directory prefix of `bucket_test/` and shipping time of 2018/7/31 17:14.

| Bucket Name | Directory Prefix | Partition Format | COS File Path |
| ----------- | -------- | ----------- | ------------------------------------------------- |
| bucket_test | logset/ | %Y/%m/%d    | bucket\_test:logset/2018/7/31\_{random}\_{index}    |
| bucket_test | logset/ | %Y%m%d/%H  | bucket\_test:logset/20180731/14\_{random}\_{index} |
| bucket_test | logset/ | %Y%m%d/log | bucket\_test:logset/20180731/log\_{random}\_{index} |

#### (Optional) Compress logs for shipping
You can compress log files before shipping. The size of an uncompressed file to be shipped is limited to 10 GB. Supported compress methods are gzip and lzop.

#### (Required) File size
It specifies the maximum size of **an uncompressed file to be shipped within the shipping interval**, which refers to the maximum size of the log file that can be shipped at the interval. A file greater than this size will be split into multiple log files. The maximum supported size is **from 100 MB to 10 GB**. 

#### (Required) Shipping interval
The shipping interval shall be **limited to 1 minute to 1 hour**. If you set it to 5 minutes, a log file is generated from your log data every 5 minutes, and multiple log files will be shipped together to your bucket at a regular interval (within half an hour). 


#### (Optional) Advanced options
Log shipping also allows you to determine whether to deliver logs based on log content, which is an advanced configuration. You can specify a key, perform regular extraction of the key's value, and set a value to match with the extracted value. A log can be delivered only when the log data matches your configuration. Unmatched logs are not delivered. As shown in the figure below, if the "action" field is set to "write", the log is delivered. You can set a maximum of 5 rules to determine whether to deliver or not. 
![](https://main.qcloudimg.com/raw/fa774d5a865c2129f707465c55e416c7.png)

>!For the log search in the mode of full text in a single line or full text in multi lines, default key is **\_CONTENT_**.

