## Overview

Through configuration in the [CLS console](https://console.cloud.tencent.com/cls), you can ship log data to COS in the JSON format. This document describes how to create a JSON log shipping task.

## Prerequisites

1. You have activated CLS, created a logset and a log topic, and successfully collected log data.
2. You have activated COS and created a bucket in the region of the log topic whose data is to be shipped. For detailed directions, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
3. Your account has the permission to configure log shipping. For how to allow sub-accounts/collaborators to configure log shipping, see the “Shipping Authorization” document.

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Log Topic** in the left sidebar.
3. Click the ID/name of the log topic whose data you want to ship.
4. Click **Ship to COS** > **Add Shipping Configuration**, and fill in the information.

**The parameters are described as follows:**
<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Format</th>
      <th>Required</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Shipping Task Name</td>
      <td>Name of a shipping task</td>
      <td nowrap="nowrap">Can contain letters, numbers, underscores (_), and hyphens (-)</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">COS Bucket</td>
      <td>Target bucket for shipping. The target bucket must be in the same region as the current log topic.</td>
      <td>Select from drop-down list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Directory Prefix</td>
      <td>Prefix of the directory under the specified COS bucket to which log files are shipped. You can customize a directory prefix. By default, log files are stored directly under the specified bucket as <code>{COS bucket}{directory prefix}{partition format}_{random}_{index}.{type}</code>, where <code>{random}_{index}</code> is a random number.</td>
			<td>Cannot start with <code>/</code></td>
      <td>No</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Partition Format</td>
      <td>A string converted from the creation time of the shipping task using the strftime function. <code>/</code> indicates directory levels.</td>
      <td>Must be in strftime format</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">File Size</td>
      <td>Maximum size of an uncompressed file to be shipped during the specified shipping interval. A log file larger than this size will be split into multiple files. The value can be from 100 MB to 256 MB.</td>
      <td nowrap="nowrap">Value range: 100-256 (MB)</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Shipping Interval</td>
      <td>Time interval of shipping, which can be 300-900 seconds. If you set it to 5 minutes, a log file will be generated from your log data every 5 minutes, and multiple log files will be shipped to your bucket at a time (with an interval of less than 30 minutes).</td>
      <td nowrap="nowrap">Value range: 300-900 (s)</td>
      <td>Yes</td>
   </tr>
</table>
 Make sure the partition format entered is in the <a href="http://man7.org/linux/man-pages/man3/strptime.3.html">strftime format</a>. Partition format affects the path to which log files are saved in COS. For example, if the target COS bucket is `bucket_test`, the directory prefix <code>logset/</code>, and the shipping time `2018/7/31 17:14`, the path to which log files are saved would vary with the partition format entered, as shown below:
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

5. Click **Next** to go to the **Advanced Configuration** page. Select **json** for **Shipping Format** and set other parameters.

**The parameters are described as follows:**
<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Format</th>
      <th>Required</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Compressed Shipping</td>
      <td>Whether to compress log files before shipping. The maximum size of an uncompressed file to be shipped is 10 GB. Log files can be compressed in GZip, Lzop, or Snappy format.</td>
      <td nowrap="nowrap">Switch</td>
      <td nowrap="nowrap">Yes</td>
   </tr>
</table>

