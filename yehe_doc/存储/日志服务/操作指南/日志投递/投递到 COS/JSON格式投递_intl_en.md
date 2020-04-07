## Overview

You can log in to the [CLS Console](https://console.cloud.tencent.com/cls) and ship JSON format data to Cloud Object Storage (COS). This topic describes how to create a JSON shipping task.


## Prerequisites

1. You have activated CLS, created a logset and a log topic, and successfully collected log data.
2. You have activated COS service and created a bucket in the target region for log topic shipping. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
3. The current account has permission to configure shipping.

## Directions

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Logset** in the left sidebar.
3. Click the name of the logset for which you want to create a shipping task.
<img src="https://main.qcloudimg.com/raw/637f191003d50812d117bd32b84b4b0d.png" width="90%">
4. In the row of the log topic to be shipped, choose **Manage** > **Shipping Configuration** to go to the **Shipping Configuration** page.
<img src="https://main.qcloudimg.com/raw/0f60de9f332b4f8192838b4f53a9994f.png" width="80%">
5. Click **Add Shipping Task** to go to the **Ship to COS** page and complete basic configuration.
<img src="https://main.qcloudimg.com/raw/b9b06dedce54cbd960fb4b6b651bdcaf.png">

**The parameters are described as follows:**

<table>
   <tr>
      <th>Parameter</th>
      <th>Description</th>
      <th>Rule</th>
      <th>Required</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Shipping Task Name</td>
      <td>Name of the shipping task.</td>
      <td nowrap="nowrap">The value can contain letters, numbers, underscores (_), and hyphens (-).</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">COS Bucket</td>
      <td>Target bucket for shipping. The target bucket must be in the same region as the current log topic.</td>
      <td>Select a value from the drop-down list.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Directory Prefix</td>
      <td>Prefix of the COS bucket directory to which log files are shipped. You can define a directory prefix. By default, log files are directly stored in the bucket, and the file path is <code>{COS bucket}{directory prefix}{partition format}_{random}_{index}.{type}</code>, where <code>{random}_{index}</code> is a random number.</td>
      <td>The value cannot begin with a slash (/).</td>
      <td>No</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Partition Format</td>
      <td>Directory automatically generated according to the creation time of the shipping task based on the strftime syntax. The slash (/) indicates a level-1 COS directory.</td>
      <td>The value must be in the strftime format.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">File Size</td>
      <td>Maximum size of an uncompressed file to be shipped during a shipping interval. A log file larger than this size will be split into multiple files. The value can be from 100 MB to 10,000 MB.</td>
      <td nowrap="nowrap">The value must be a number ranging from 100 to 10,000 (unit: MB).</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Shipping Interval</td>
      <td>Time interval for shipping. If you set it to 5 minutes, a log file is generated for your log data every 5 minutes, and the log files generated will be shipped together to your bucket at a regular interval (within half an hour).</td>
      <td nowrap="nowrap">The value must be a number ranging from 60 to 3,600 (unit: seconds).</td>
      <td>Yes</td>
   </tr>
</table>

Enter partition formats based on the requirements of the [strftime format](http://man7.org/linux/man-pages/man3/strptime.3.html). Different partition formats may affect the paths of files shipped to COS. The following example describes how to use partition formats. For example, if a file is shipped to the `bucket_test` bucket, the directory prefix is `logset/`, and the shipping time is 2018/7/31 17:14, the corresponding shipping file path is as follows:

| Bucket Name  | Directory Prefix | Partition Format   | COS File Path                                     |
| ----------- | -------- | ---------- | ------------------------------------------------ |
| bucket_test | logset/  | %Y/%m/%d   | bucket_test:logset/2018/7/31_{random}_{index}    |
| bucket_test | logset/  | %Y%m%d/%H  | bucket_test:logset/20180731/14_{random}_{index}  |
| bucket_test | logset/  | %Y%m%d/log | bucket_test:logset/20180731/log_{random}_{index} |

6. Click **Next** to go to the **Advanced Configuration** page. Set **Shipping Format** to **json** and set other parameters.
   <img src="https://main.qcloudimg.com/raw/d9bfb3a445921c658d9ad20139f9fc14.png">

**The parameters are described as follows:**

<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Rule</th>
      <th>Required</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Compressed Shipping</td>
      <td>You can determine whether to compress log files before shipping. The size of an uncompressed file to be shipped is limited to 10 GB. Log files can be compressed using gzip, lzop, or Snappy.</td>
      <td nowrap="nowrap">Enabled/Disabled</td>
      <td nowrap="nowrap">Yes</td>
   </tr>
</table>

**(Optional) Advanced Options**
You can enable **Advanced Options** to filter logs based on log content before shipping.
>Up to 5 shipping filtering rules are allowed, among rules is “And” logic, i.e. log files are shipped only when all the rules are met.
>
a. Specify a key and set a filtering rule to perform RegEx extraction on the key.
b. Use "()" to capture objects that need to match the value and enter the value to match. The system performs a match according to the regular expression in the shipping rule, extracts the content of the capture group "()", and compares it with the value. If the captured content is equal to the value, the log data will be shipped.
**Sample 1:**
Set the field name to `status`, with the key-value pair similar to `status:404`. If you want to ship the log where the value of the `status` field is `404`, set the filtering rule to `(.*)`.
![](https://main.qcloudimg.com/raw/f2951b74963fb46f8bc21598db1bc50d.png)

**Sample 2:**
Set the field name to `http_host`, with the key-value pair is similar `http_host:172.16.19.20`. If you want to ship the log where the value of the `http_host` field starts with `172.16`, set the filtering rule to `^(\d+\.\d+)\..*`.
![](https://main.qcloudimg.com/raw/06be27e1f831177a081805deb6b07e7a.png)
7. Click **OK**. The shipping task is enabled.
   <img src="https://main.qcloudimg.com/raw/f7e01dbd1b3cffbd26c2e3f7f4452ffd.png" width="90%">

