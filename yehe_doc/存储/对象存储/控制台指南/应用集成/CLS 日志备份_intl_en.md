## Overview

The CLS log backup feature is provided by COS based on [SCF](https://www.tencentcloud.com/document/product/583) to dump CLS logs to COS.

After you configure a log backup rule for a bucket, SCF will dump the CLS logs to the bucket according to the time granularity configured.

CLS log backup can ship log data to COS to further meet the needs of log backup scenarios and harness the value of log data. Log backup is an asynchronous process. When log data is generated, SCF automatically backs up the log data to COS for storage via trigger.



## Notes

- If you have previously added a CLS log backup rule to your bucket via the COS console, you can view the CLS log backup function you created in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
CLS log backup is supported in SCF-enabled regions, including Guangzhou, Shanghai, Beijing, Hong Kong (China), Chengdu, Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see the [SCF documentation](https://www.tencentcloud.com/document/product/583).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Application Integration** > **Data Backup** and find **CLS Log Backup**.
3. Click **Configure Backup Rule** to go to the rule configuration page.
4. Click **Add Function**.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
5. In the pop-up window, configure the following items:

	- **Function Name**: Uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
	- **Associated Bucket**: A COS bucket that stores the CLS logs.
	- **Logset**: A [logset](https://intl.cloud.tencent.com/document/product/614/32849) is a project management unit of CLS, used to distinguish logs of different projects. You can select the logset of the message source, which must be in the function region.
	- **Log Topic**: A log topic is the basic management unit of CLS and also the smallest unit for managing and configuring CLS triggers. A logset can contain multiple log topics. You can select a log topic of the message source.
	- **Max Wait Time**: You can set this parameter to control the log obtaining frequency. The parameter value can range from 3 to 300 seconds. If you set the parameter to 300 seconds, the SCF will collect the log data generated within 300 seconds and package it centrally as log files for backup.
	- **SCF Authorization**: SCF needs to be authorized to read CLS logs and dump them to the specified bucket.
6. Click **Next** to configure the following information:

	- **Compression Format**: You can determine whether to compress log files before backup. A compressed log file can be up to 128 KB. Currently, log files can be compressed using gzip, lzop or snappy.
	- **Partition Format**: A directory is automatically generated based on the strftime syntax. For example, if the partition format is `%Y/%m/%d/%Y%m%d%H%M`, the generated directory is `2021/06/25/202106252232`.
	- **Delivery Path**: Log backup path. You can select the root directory or specify a path prefix.
	- **Delivery Sample**: The final backup filename is in the format of `{COS bucket}{Directory prefix}{Partition format}_{random}.{type}`.
7. Click **Confirm**. After the CLS backup rule is created, you can view it in the list.

   You can perform the following operations on the created CLS log backup rule:
	- Click **Log** to view the historical running status of CLS log backup. If an error is reported, you can click **Log** to quickly redirect to the SCF console for viewing the error log details.
	- Click **More** > **Edit** to modify the CLS log backup rule.
	- Click **More** > **Delete** to delete the unwanted CLS log backup rule.
