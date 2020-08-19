## Overview

You can log in to the [Cloud Log Service Console](https://console.cloud.tencent.com/cls) and ship data of the separator format to Cloud Object Storage (COS). This document describes how to create a separator-based log shipping task.


## Prerequisites
1. You have activated the Cloud Log Service (CLS), created a logset and a log topic, and successfully collected the log data.
2. You have activated COS and created a bucket in the destination region of the log topic shipping. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
3. Make sure that the current account has the permission to configure shipping.


## Directions

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Logset** in the left sidebar.
3. On the **Logset Management** page, click the target logset ID/name to go to its details page.
4. Locate the log topic to be shipped, and choose **Manage** -> **Shipping Configuration** to go to the **Shipping Configuration** page.
5. Click **Add Shipping Task** to go to the **Ship to COS** page and enter the configuration information in order.
**The configuration items are described as follows:**

<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Rule</th>
      <th>Required or Not</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Shipping Task Name</td>
      <td>Configures the name of a shipping task.</td>
      <td nowrap="nowrap">The name can contain letters, numbers, underscores (_), and hyphens (-).</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">COS Bucket</td>
      <td>Target bucket for shipping. The target bucket must be in the same region as the current log topic.</td>
      <td>A value selected from the drop-down list.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Directory Prefix</td>
      <td>Prefix of the COS bucket directory to which log files are shipped. You can define a directory prefix. By default, log files are directly stored in the bucket, and the file path is <code>{COS bucket}{directory prefix}{partition format}_{random}_{index}.{type}</code>, where <code>{random}_{index}</code> is a random number.</td>
      <td>Not starting with a forward slash (/)</td>
      <td>No</td>
   </tr>
   <tr>
      <td>Partition Format</td>
      <td>Directory automatically generated according to the creation time of the shipping task based on the strftime syntax. The slash (/) indicates a level-1 COS directory.</td>
      <td>strftime format</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">File Size</td>
      <td>Maximum size of an uncompressed file to be shipped during a shipping interval. A log file larger than this size will be split into multiple files. The value can be from 100 MB to 10,000 MB.</td>
      <td nowrap="nowrap">100 MB to 10,000 MB</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Shipping Interval</td>
      <td>Specifies the time interval of shipping, which can be from 60 seconds to 3,600 seconds. If you set it to 5 minutes, a log file is generated from your log data every 5 minutes, and multiple log files will be shipped together to your bucket at a regular interval (within half an hour).</td>
      <td>60 seconds to 3,600 seconds</td>
      <td>Yes</td>
   </tr>
</table>

Enter partition formats based on the requirements of the [strftime format](http://man7.org/linux/man-pages/man3/strptime.3.html). Different partition formats may affect the paths of files shipped to COS. The following example describes how to use partition formats. For example, if a file is shipped to the `bucket_test` bucket, the directory prefix is `logset/`, and the shipping time is 2018/7/31 17:14, the corresponding shipping file path is as follows:

| Bucket Name | Directory Prefix | Partition Format | COS File Path |
| ----------- | -------- | ---------- | ------------------------------------------------ |
| bucket_test | logset/ | %Y/%m/%d | bucket_test:logset/2018/7/31_{random}_{index} |
| bucket_test | logset/ | %Y%m%d/%H  | bucket_test:logset/20180731/14_{random}_{index} |
| bucket_test | logset/ | %Y%m%d/log | bucket_test:logset/20180731/log_{random}_{index} |

6. Click **Next** to go to the advanced configuration page. Set **Shipping Format** to **CSV** and enter the relevant parameters in order.
 **The configuration items are described as follows:**

<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Rule</th>
      <th>Required or Not</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Key</td>
      <td>Specifies the `Key` field of the written CSV file. (The value must be the key name or reserved field after logs are structured. Otherwise, the key is invalid.)</td>
      <td nowrap="nowrap">The value can contain letters, numbers, underscores (_), and hyphens (-).</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Separator</td>
      <td>Separators between the fields in the CSV file.</td>
      <td>A value selected from the drop-down list.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Escape character</td>
      <td> If a value field contains the selected separator characters, the separator characters will be enclosed by escape characters to prevent incorrect identification during data reading.</td>
      <td>A value selected from the drop-down list.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Invalid Field Filling</td>
      <td>If the configured value of the `Key` field is invalid, this field will be set.</td>
      <td>A value selected from the drop-down list.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Key in First Line</td>
      <td>Adds field name description to the first line of the CSV file. That is, the key value is written into the first line of the CSV file (disabled by default).</td>
      <td>Enabled/Disabled</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Compressed Delivery</td>
      <td>You can determine whether to compress log files before shipping. The size of an uncompressed file to be shipped is limited to 10 GB. Log files can be compressed using gzip, lzop, or Snappy.</td>
      <td>Enabled/Disabled</td>
      <td>Yes</td>
   </tr>
</table>

**(Optional) Advanced Options**
You can enable **Advanced Options** to filter logs based on log content before shipping.
>Up to 5 shipping filtering rules are allowed, among rules is “And” logic, i.e. log files are shipped only when all the rules are met.
>
a. Specify a key and set a filtering rule to perform RegEx extraction on the key.
b. Use "()" to capture objects that need to match the value and enter the value to match. The system performs a match according to the regular expression in the shipping rule, extracts the content of the capture group "()", and compares it with the value. If the captured content is equal to the value, the log data will be shipped.
Sample 1:
Specify a field as `status`. For example, the key-value pair is `status:404`. If you want to ship logs with a status field of 404, the filtering rule is `(.*)`.
Sample 2:
Specify a field as `http_host`. For example, the key-value pair is `http_host:172.16.19.20`. If you want to ship logs with an `http_host` field starting with “172.16”, the filtering rule is `^(\d+\.\d+)\..*`.
7. Click **OK** to enable shipping.
