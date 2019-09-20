## Overview

You can log in to the [CLS Console](https://console.cloud.tencent.com/cls) and ship data of the JSON format to Cloud Object Storage (COS). This topic describes how to create a task of shipping data of the JSON format.


## Prerequisites

1. You have activated CLS, created a logset and a log topic, and successfully collected the log data.
2. You have activated COS and created a bucket in the target region of the log topic shipping. For more information, see [Creating Bucket](https://intl.cloud.tencent.com/document/product/436/13309).
3. You have to ensure that the current account has the permission to configure shipping tasks.

## Directions

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Logset Management** in the left sidebar.
3. Click on the logset ID/name for which you want to set shipping tasks to go to its details page.
![](https://main.qcloudimg.com/raw/c5781d2d437c290f00c0ece75a2691dd.png)
4. Locate the log topic to be shipped, click **Configure** -> **Shipping to COS Configuration** to go to the **Shipping Configuration** page.
![](https://main.qcloudimg.com/raw/0f60de9f332b4f8192838b4f53a9994f.png)
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
      <td>The bucket in the same region as the current log topic is used as the target bucket for shipping.</td>
      <td>A value selected from the list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Directory prefix</td>
      <td>CLS allows you to define a directory prefix. Log files are shipped to the directory of the COS bucket. Log files are stored in the bucket by default with the path <code>{COS bucket}{directory prefix}{partition format}_{random}_{index}.{type}</code>, where <code>{random}_{index}</code> is a random number.</td>
      <td>Not starting with a forward slash (/)</td>
      <td>No</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Partition Format</td>
      <td>Automatically generates a directory for the shipping task creation time based on the strftime syntax. The forward slash (/) represents a level-1 COS directory.</td>
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
      <td>Shipping Interval</td>
      <td>Specifies the time interval of shipping. It currently supports from 60 seconds to 3,600 seconds. If you set it to 5 minutes, a log file is generated from your log data every 5 minutes, and multiple log files will be shipped together to your bucket at a regular interval (within half an hour).</td>
      <td nowrap="nowrap">60 seconds to 3,600 seconds</td>
      <td>Yes</td>
   </tr>
</table>

Enter partition formats based on the requirements of the [strftime format](http://man7.org/linux/man-pages/man3/strptime.3.html). Different partition formats may affect the paths of files shipped to COS. The following example describes how to use partition formats. For example, if a file is shipped to the bucket_test bucket, the directory prefix is `logset/`, and the shipping time is 2018/7/31 17:14, the corresponding shipping file path is as follows:

| Bucket Name  | Directory prefix | Partition Format   | COS File Path                                     |
| ----------- | -------- | ---------- | ------------------------------------------------ |
| bucket_test | logset/  | %Y/%m/%d   | bucket_test:logset/2018/7/31_{random}_{index}    |
| bucket_test | logset/  | %Y%m%d/%H  | bucket_test:logset/20180731/14_{random}_{index}  |
| bucket_test | logset/  | %Y%m%d/log | bucket_test:logset/20180731/log_{random}_{index} |

6. Click **Next** to go to the advanced configuration page. Set the shipping format to JSON and enter relevant parameters successively.
![](https://main.qcloudimg.com/raw/d9bfb3a445921c658d9ad20139f9fc14.png)

**The configuration items are as follows:**

<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Rule</th>
      <th>Required or Not</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Compressed Shipping</td>
      <td>You can determine whether to compress log files before shipping. The size of an uncompressed file to be shipped is limited to 10 GB. Files can be compressed into a GZIP or LZOP package.</td>
      <td nowrap="nowrap">Enabled/Disabled</td>
      <td nowrap="nowrap">Yes</td>
   </tr>
</table>

**Advanced Options** (Optional)
You can open **Advanced Options** to filter logs based on log content before shipping.
You can specify a key, perform regular RegEx extraction of the corresponding values, and specify values to be matched from the extracted value. A log can be shipped only when the log data matches your configuration. Unmatched logs are not shipped.
As shown below, if the `action` field is set to `write`, the log is shipped. Up to 5 shipping filtering rules are supported.
![](https://main.qcloudimg.com/raw/b8baf9009d52bb7aaa01eab24b65e4b8.png)
7. Click **OK**. The shipping is then enabled.
![](https://main.qcloudimg.com/raw/f7e01dbd1b3cffbd26c2e3f7f4452ffd.png)
