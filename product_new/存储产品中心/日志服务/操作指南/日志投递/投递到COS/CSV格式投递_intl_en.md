## Overview

You can log in to the [CLS Console](https://console.cloud.tencent.com/cls) and ship data of the CSV format to Cloud Object Storage (COS). This topic describes how to create a CSV shipping task.


## Prerequisites
1. You have activated CLS, created a logset and a log topic, and successfully collected the log data.
2. You have activated COS and created a bucket in the target region of the log topic shipping. For more information, see [Creating Bucket](https://intl.cloud.tencent.com/document/product/436/13309).
3. You have to ensure that the current account has the permission to configure shipping tasks.


## Directions

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Logset Management** in the left sidebar.
3. Click on the logset ID/name for which you want to set shipping tasks to go to its details page.
![](https://main.qcloudimg.com/raw/867bf17736b5dda680cba78e4dbdca5b.png)
4. Locate the log topic to be shipped, click **Configure** -> **Shipping to COS Configuration** to go to the **Shipping Configuration** page.
![](https://main.qcloudimg.com/raw/a8cd06e71f91561f1e74073dc9e00a9b.png)
5. Click **Add Shipping Configuration** to go to the **Ship to COS** page and enter the configuration information successively.
![](https://main.qcloudimg.com/raw/b9b06dedce54cbd960fb4b6b651bdcaf.png)
**The configuration items are as follows:**

<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Rule</th>
      <th>Required or Not</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Shipping Task Name</td>
      <td>Sets the name of a shipping task.</td>
      <td nowrap="nowrap">Letters, numbers, underscores (_), and hyphens (-)</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">COS Bucket</td>
      <td>Use the bucket in the same region as the current log topic as the target bucket for shipping.</td>
      <td>A value selected from the list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Directory prefix</td>
      <td>CLS allows you to define a directory prefix. Log files are shipped to the directory of the COS bucket. Log files are stored in the bucket by default under the path <code>{COS bucket}{directory prefix}{partition format}_{random}_{index}.{type}</code>, where <code>{random}_{index}</code> is a random number.</td>
      <td>Not starting with a forward slash (/)</td>
      <td>No</td>
   </tr>
   <tr>
      <td>Partition Format</td>
      <td>Automatically generates a directory for the shipping task creation time based on the strftime syntax. The forward slash (/) represents a level of COS directory.</td>
      <td>strftime format</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">File Size</td>
      <td>Specifies the maximum size of an uncompressed file to be shipped during a shipping interval. It means that during the time interval, the maximum size of the log file that can be shipped is the value you set. A file larger than this size will be split into multiple log files. The value should be from 100 MB to 10,000 MB.</td>
      <td nowrap="nowrap">100 MB to 10,000 MB</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Shipping Interval</td>
      <td>Specifies the time interval of shipping. It currently supports from 60 seconds to 3,600 seconds. If you set it to 5 minutes, a log file is generated from your log data every 5 minutes, and multiple log files will be shipped together to your bucket at a regular interval (within half an hour).</td>
      <td>60 seconds to 3,600 seconds</td>
      <td>Yes</td>
   </tr>
</table>

Enter partition formats based on the requirements of the [strftime format](http://man7.org/linux/man-pages/man3/strptime.3.html). Different partition formats may affect the paths of files shipped to COS. The following example describes how to use partition formats. For example, if a file is shipped to the bucket_test bucket, the directory prefix is `logset/`, and the shipping time is 2018/7/31 17:14, the corresponding shipping file path is as follows:

| Bucket Name  | Directory prefix | Partition Format   | COS File Path                                     |
| ----------- | -------- | ---------- | ------------------------------------------------ |
| bucket_test | logset/  | %Y/%m/%d   | bucket_test:logset/2018/7/31_{random}_{index}    |
| bucket_test | logset/  | %Y%m%d/%H  | bucket_test:logset/20180731/14_{random}_{index}  |
| bucket_test | logset/  | %Y%m%d/log | bucket_test:logset/20180731/log_{random}_{index} |

6. Click **Next** to access the advanced configuration page. Set **Shipping Format** to **CSV** and enter relevant parameters successively.
![img](https://main.qcloudimg.com/raw/44bc07a3d69496a59fb81fb8730cc2e3.png)
 **The configuration items are as follows:**

<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Rule</th>
      <th>Required or Not</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Key name</td>
      <td>Specifies the `key` field of the written CSV file. (The value must be the key name or reserved field after logs are structured. Otherwise, the key is invalid.)</td>
      <td nowrap="nowrap">Letters, numbers, underscores (_), and hyphens (-)</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Separator</td>
      <td>Separators between the fields in a CSV file.</td>
      <td>A value selected from the list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Escape character</td>
      <td> If the value fields contain the selected separator characters, the separators will be enclosed by escape characters to prevent incorrect identification during data reading.</td>
      <td>A value selected from the list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Invalid Field</td>
      <td>If the value of the `key` field is invalid, it will be filled with an invalid field.</td>
      <td>A value selected from the list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Key in First Line</td>
      <td>Field name description is added to the first line of the CSV file. That is, keys are written into the first line of the CSV file (disabled by default).</td>
      <td>Enabled/Disabled</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Compressed Shipping</td>
      <td>You can determine whether to compress log files before shipping. The size of an uncompressed file to be shipped is limited to 10 GB. Files can be compressed into a GZIP or LZOP package.</td>
      <td>Enabled/Disabled</td>
      <td>Yes</td>
   </tr>
</table>

**Advanced Options**(Optional)
You can open **Advanced Options** to filter logs based on log content before shipping.
>Up to 5 shipping filtering rules are allowed, among rules is “And” logic, i.e. the log can be shipped only when it meet all rules.
>
a. Specify a key, and perform RegEx extraction on it by setting filtering rules.
b. Use “()” to capture objects that needs to match the value and enter the value to match. The system first performs a match according to the regular expressions in shipping rule, extracts the content of the capture group "()", and compares it with the value. When the captured content is equal to the value, the log data will be shipped.
Sample 1:
Specify a field as `status`. For example, the key-value pair is `status: 404`. If you want to ship the log with a status field of 404, the filtering rule is `(.*)`
![](https://main.qcloudimg.com/raw/f2951b74963fb46f8bc21598db1bc50d.png)
Sample 2:
Specify a field as `http_host`. For example, the key-value pair is `http_host:172.16.19.20`. If you want to ship the log with a http_host field start with “172.16”, the filtering rule is `^(\d+\.\d+)\..*`.
![](https://main.qcloudimg.com/raw/06be27e1f831177a081805deb6b07e7a.png)
7. Click **OK**. The shipping is then enabled.
![](https://main.qcloudimg.com/raw/aa06986067d5d7c13fe4e681d2d2285f.png)
