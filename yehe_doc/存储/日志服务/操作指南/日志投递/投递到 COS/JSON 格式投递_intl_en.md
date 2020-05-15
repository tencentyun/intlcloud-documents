## Overview

You can ship JSON data to Cloud Object Storage (COS) through the [Cloud Log Service Console](https://console.cloud.tencent.com/cls). This topic describes how to create a JSON shipping task.

## Prerequisites

1. You have activated CLS, created a logset and a log topic, and successfully collected log data.
2. You have activated COS service and created a bucket in the target region for log topic shipping. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
3. The current account has the permission to configure shipping tasks.

## Directions

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Logset** in the left sidebar.
3. Click the name of the logset for which you want to create a shipping task.
   <img src="https://main.qcloudimg.com/raw/c5781d2d437c290f00c0ece75a2691dd.png" width="80%">
4. In the row of the log topic to be shipped, choose **Manage** -> **Shipping Configuration** to go to the **Shipping Configuration** page.
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
      <td>The name of a shipping task.</td>
      <td nowrap="nowrap">The name contains letters, numbers, underscores (_), or hyphens (-).</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">COS Bucket</td>
      <td>Target bucket for shipping. The target bucket must be in the same region as the current log topic.</td>
      <td>Select a value from the drop-down list.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Directory prefix</td>
      <td>Prefix of the COS bucket directory to which log files are shipped. You can define a directory prefix. By default, log files are directly stored at <code>{COS bucket}{directory prefix}{partition format}_{random}_{index}.{type}</code> in the bucket, where <code>{random}_{index}</code> is a random number.</td>
			<td>The directory prefix cannot start with a slash (<code>/</code>)</td>
      <td>No</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Partition Format</td>
      <td>Directory automatically generated according to the creation time of the shipping task based on the strftime syntax. The slash (<code>/</code>) indicates a level-1 COS directory.</td>
      <td>The value must be in the strftime format.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">File Size</td>
      <td>Maximum size of an uncompressed file to be shipped over a shipping interval. A log file larger than this value will be split into multiple files with a size ranging from 100 MB to 256 MB.</td>
      <td nowrap="nowrap">The value must be a number ranging from 100 to 256 (unit: MB).</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Shipping Interval</td>
      <td>Time interval for shipping, ranging from 300s to 900s. If you set it to 5 minutes, a log file is generated for your log data every 5 minutes, and the log files generated will be shipped together to your bucket at a regular interval (within half an hour).</td>
      <td nowrap="nowrap">The value must be a number ranging from 300 to 900 (unit: seconds).</td>
      <td>Yes</td>
   </tr>
</table>



Enter partition formats based on the requirements of the [strftime format](http://man7.org/linux/man-pages/man3/strptime.3.html). Different partition formats may affect the paths of files shipped to COS. The following example describes how to use partition formats. For example, if a file is shipped to `logset/` of the `bucket_test` bucket at 17:14 on 2018/7/31, the corresponding shipping file path is as follows:

| Bucket Name | Directory Prefix | Partition Format | COS File Path |
| ----------- | -------- | ---------- | ------------------------------------------------ |
| bucket_test | logset/  | %Y/%m/%d   | bucket_test:logset/2018/7/31_{random}_{index}    |
| bucket_test | logset/  | %Y%m%d/%H  | bucket_test:logset/20180731/14_{random}_{index}  |
| bucket_test | logset/  | %Y%m%d/log | bucket_test:logset/20180731/log_{random}_{index} |

6. Click **Next** to go to the **Advanced Configuration** page. Set **Shipping Format** to **json** and set other parameters.
   <img src="https://main.qcloudimg.com/raw/d9bfb3a445921c658d9ad20139f9fc14.png">

**The parameters are described as follows:**

<table>
   <tr>
      <th>Parameter</th>
      <th>Description</th>
      <th>Rule</th>
      <th>Required</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Compressed Delivery</td>
      <td>You can determine whether to compress log files before shipping. The size of an uncompressed file to be shipped is limited to 10 GB. Log files can be compressed using gzip, lzop, or snappy.</td>
      <td nowrap="nowrap">Enabled/Disabled</td>
      <td nowrap="nowrap">Yes</td>
   </tr>
</table>

