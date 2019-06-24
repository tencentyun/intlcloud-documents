## Introduction
CLS can ship logs to Cloud Object Storage (COS) for long-term log data storage. By making configuration in the console, logs can be shipped to COS according to preset shipping intervals, file sizes, paths and filtering rules.

## Directions
### Prerequisites

1. Activate the CLS, create a logset and a log topic, and the log data can be successfully collected.
2. Activate Tencent Cloud COS and create a bucket in the region logset will be shipped to.
3. Make sure that the current account has the permission to configure shipping. 

### Procedure
1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Logset** in the left navigation pane.
3. Select the logset to which a shipping task needs to be added, click the logset ID/name to go to its details page.
![](https://main.qcloudimg.com/raw/1c7469782437b6c377b8108877e78899.png)
4. Locate the log topic to be shipped, click **Configure** -> **Shipping to COS Configuration** to go to the "Shipping Configuration" page.
![](https://main.qcloudimg.com/raw/0ad3f1f23c67bcb53974b94e12549727.png)
5. Click **Add Shipping Task** to go to the **Ship to COS** page to complete the configuration information, and then click **Next**. 
![](https://main.qcloudimg.com/raw/9ee68687e345cd24e352e47895e08762.png)
6. Go to **Advanced Configuration** and select the shipping format, whether to enable compressed delivery, compression format, and shipping filter.
If you select json, you need to make the following configurations:
![](https://main.qcloudimg.com/raw/8af28118ae8445dc4a173310bbd2a747.png)
If you select csv, you need to specify the key, separator, escape character, invalid field content, whether to write the key into the first line, etc.
![](https://main.qcloudimg.com/raw/77f75aff5524f06d705f02848ea74592.png)
 - Key: The key field written to the csv file.
 - Separator: Separators between the fields in the csv file.
 - Escape Character: If the value fields contain the selected separator characters, the separators will be enclosed by escape characters.
 - Invalid Field Filling: If the configured CSV key-value field is an invalid key, the invalid field will be filled.
 - Key in First Line: Write the keys into the first line of CSV file (disabled by default).
7. Check if the shipping status is enabled.
![](https://main.qcloudimg.com/raw/5156e3f409bfe76afcb27bbeac7b0585.png)

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
Log shipping also allows you to determine whether to deliver logs based on log content, which is an advanced configuration. You can specify a key, perform regular extraction of the key's value, and set a value to match with the extracted value. A log can be delivered only when the log data matches your configuration. Unmatched logs will not be delivered. As shown in the figure below, if the "action" field is set to "write", log will be delivered. You can set up to 5 filter rules.
![](https://main.qcloudimg.com/raw/273963759377765714ef2612e4829970.png)

>For the log search in the mode of full text in a single line or full text in multi lines, default key is **\_CONTENT_**.

