## Overview

You can log in to the [CLS console](https://console.cloud.tencent.com/cls) and ship Comma Separated Values (CSV)-formatted data to COS. This document describes how to create a CSV-formatted log shipping task.

## Prerequisites

1. You have activated CLS, created a logset and a log topic, and successfully collected the log data.
2. You have activated COS service and created a bucket in the target region for log topic shipping. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
3. You have ensured that the current account has permission to configure shipping tasks.

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Log Topic** in the left sidebar.
3. Click the desired log topic ID/name to go to the log topic management page.
4. Click **Ship to COS**, click **Add Shipping Configuration**, and then finish the configuration.
**The configuration items are described as follows:**
<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Limit</th>
      <th>Required</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Shipping Task Name</td>
      <td>Configures the name of a shipping task</td>
      <td nowrap="nowrap">The name can contain letters, numbers, underscores (_), and hyphens (-)</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">COS Bucket</td>
      <td>Target bucket for shipping. The target bucket must be in the same region as the current log topic.</td>
      <td>A value selected from the drop-down list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Directory Prefix</td>
      <td>Prefix of the COS bucket directory to which log files are shipped. You can define a directory prefix. By default, log files are directly stored in the bucket, and the file path is <code>{COS bucket}{directory prefix}{partition format}_{random}_{index}.{type}</code>, where <code>{random}_{index}</code> is a random number.</td>
      <td>Cannot start with <code>/</code></td>
      <td>No</td>
   </tr>
   <tr>
      <td>Partition Format</td>
			<td>The directory will be automatically generated according to the creation time of the shipping task based on the strftime syntax. The forward slash (/) represents a level of COS directory.</td>
      <td>The value must be in strftime format</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">File Size</td>
      <td>Maximum size of an uncompressed file to be shipped during a shipping interval. A log file larger than this size will be split into multiple files. The value can be from 100 MB to 256 MB.</td>
      <td nowrap="nowrap">Value range: 100-256 MB</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Shipping Interval</td>
      <td>Specifies the time interval of shipping, which can be from 300s - 900s. If you set it to 5 minutes, a log file is generated from your log data every 5 minutes, and multiple log files will be shipped together to your bucket at a regular interval (within half an hour).</td>
      <td>Value range: 300-900s</td>
      <td>Yes</td>
   </tr>
</table>
Enter partition formats based on the requirements of the [strftime format](http://man7.org/linux/man-pages/man3/strptime.3.html). Different partition formats may affect the paths of files shipped to COS. The following example describes how to use partition formats. For example, if a file is shipped to the `bucket_test` bucket, the directory prefix is `logset/`, and the shipping time is `2018/7/31 17:14`, the corresponding shipping file path is as follows:
<table>
<thead>
<tr><th>Bucket</th><th>Directory Prefix</th><th>Partition Format</th><th>COS File Path</th></tr>
</thead>
<tbody>
	<tr>
		<td>bucket_test</td>
		<td>logset/</td>
		<td>%Y/%m/%d</td>
		<td>bucket_test:logset/2018/7/31_{random}_{index}</td>
	</tr>
	<tr>
		<td>bucket_test</td>
		<td>logset/</td>
		<td>%Y%m%d/%H</td>
		<td>bucket_test:logset/20180731/14_{random}_{index}</td>
	</tr>
	<tr>
		<td>bucket_test</td>
		<td>logset/</td>
		<td>%Y%m%d/log</td>
		<td>bucket_test:logset/20180731/log_{random}_{index}</td>
	</tr>
</tbody></table>
5. Click **Next** to go to the advanced configuration page. Set **Shipping Format** to **CSV** and enter the relevant parameters in order.
![img](https://main.qcloudimg.com/raw/b9b06dedce54cbd960fb4b6b651bdcaf.png)
**The configuration items are described as follows:**
<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Limit</th>
      <th>Required</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Key</td>
      <td>Specifies the key name of the written CSV file. The value must be the key name or reserved parameter after logs are structured. Otherwise, the value is invalid.</td>
      <td nowrap="nowrap">The value can contain letters, numbers, underscores (_), and hyphens (-)</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Separator</td>
      <td>Separators between the fields in the CSV file</td>
      <td>A value selected from the drop-down list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Escape Character</td>
      <td> If a value field contains the selected separator characters, the separator characters will be enclosed by escape characters to prevent incorrect identification during data reading.</td>
      <td>A value selected from the drop-down list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Invalid Field Filling</td>
      <td>This field will be used if the configured key name is invalid. </td>
      <td>A value selected from the drop-down list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Key in First Line</td>
      <td>Adds field name description to the first line of the CSV file. That is, the key value is written into the first line of the CSV file. This is disabled by default.</td>
      <td>Enabled/Disabled</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Compressed Delivery</td>
      <td>You can determine whether to compress log files before shipping. The size of an uncompressed file to be shipped is limited to 10 GB. Log files can be compressed in GZip, Lzop or Snappy format.</td>
      <td>Enabled/Disabled</td>
      <td>Yes</td>
   </tr>
</table>

