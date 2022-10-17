## Overview

Cloud Log Service (CLS) provides a one-stop log data solution. You can quickly and conveniently connect to it in five minutes to enjoy a full range of stable and reliable services from log collection, storage, and processing to search, analysis, consumption, shipping, dashboard generation, and alarming, with no need to care about resource issues such as scaling. It helps you improve the problem locating and metric monitoring efficiency in an all-around manner, making log Ops much easier.

This document describes how to use basic CLS features:
- Collect log files from servers with LogListener
- Search for and analyze logs

If you don't have proper resources to collect logs, you can use [demos](https://intl.cloud.tencent.com/document/product/614/43572) to quickly try out CLS's log search and analysis, dashboard, and alarming features free of charge without collecting logs.


## Step 1. Activate the service

Log in to the [Tencent Cloud CLS console](https://console.cloud.tencent.com/cls/overview). If CLS is not activated for your account, you will be prompted for activation. Just click **Activate**.

## Step 2. Install LogListener

LogListener collects log files to CLS. The following describes how to install it in a Tencent Cloud CVM/Lighthouse instance.
LogListener also supports [non-Tencent Cloud servers](https://intl.cloud.tencent.com/document/product/614/17414), [TKE](https://intl.cloud.tencent.com/document/product/457/32419), and [self-built K8s clusters](https://intl.cloud.tencent.com/document/product/614/42745).

#### Step 2.1. Get the key

Go to the [CAM console](https://console.cloud.tencent.com/cam/capi), view/create and record the key, and make sure that the key is enabled.

#### Step 2.2. Install LogListener

1. On the [Machine Group Management](https://console.cloud.tencent.com/cls/hosts) page, switch to the target CVM/LightHouse region in the top-left corner and click **Deploy Instances** in the top-right corner.

2. Select the target instance, enter the `SecretId` and `SecretKey` obtained in step 2.1 in **Enter a SecretId**, and enter **Machine label** (such as `test`, which is similar to an instance category for subsequent batch log collection from multiple machines).

3. After the installation is completed, click **Next**.

4. Add the instance with LogListener installed to a new machine group that requires log collection. Log files under the same path can be batch collected for instances in the same group. Enter the **Machine Group Name** and click **Join**.


## Step 3. Create a log topic

A log topic is the basic unit for log data collection, storage, search, and analysis. It usually corresponds to a certain application/service (with a similar log structure). Log topics can be grouped by logset. A logset doesn't store any log data and is only used to facilitate log topic management.

1. On the [Log Topic](https://console.cloud.tencent.com/cls/topic) page, switch to the region in step 2.2 in the top-left corner and click **Create Log Topic**.

2. In the pop-up window, enter information and click **OK**.

 - Log Topic Name: `test` for example
 - Storage Class: STANDARD
 - Logset Operation: **Create Logset**
 - Logset Name: `test` for example

## Step 4. Configure collection rules and indexes

1. On the [Log Topic](https://console.cloud.tencent.com/cls/topic) page, click the **Log Topic Name/ID** in step 3.
2. Select the **Collection Configuration** tab and click **Add** in the **LogListener Collection Configuration** area.

3. On the **Log Data Source** page, select ** Logs with Full Text in a Single Line**.

>?
> - If you select **Logs with Full Text in a Single Line**, raw logs will be directly reported to CLS, and log fields won't be segmented or extracted. This is a simple way of extraction suitable for getting started with CLS, but it may prevent you from using features such as log search and analysis (for example, log search by field or statistical log analysis). In actual use, we recommend you select a proper log format to segment and extract log fields as instructed in [Collection Overview](https://intl.cloud.tencent.com/document/product/614/31652).
> - For JSON logs, you can select **JSON Log File**.
> 
4. Select the machine group created in step 2.2 and click **Next**.

5. Enter the **Collection Rule Name** and **Collection Path** (i.e., the path of the target log file) and click **Next**.
For example, if the absolute path of the target file is `/root/test.log`, then the **Directory Prefix** for **Collection Path** should be `/root`, and the file name should be `test.log`.

6. Set the index configuration and enable full-text index.

>?
> - If **Extraction Mode** is not **Full text in a single line**, you can enable **Key-Value Index** and click **Auto Configure** to automatically configure the key-value index for the collected logs.
> - The modified index configuration takes effect only for newly written logs. Existing data won't be updated.
> - For more information on index configuration items, see [Configuring Index](https://intl.cloud.tencent.com/document/product/614/39594).
> 

## Step 5. Search for and analyze logs

1. On the [Search and Analysis](https://console.cloud.tencent.com/cls/search) page, select the log topic created in step 3 at the top to view the collected log data.

2. In the input box at the top, enter the target text as the search condition and click **Search and Analysis** to search for logs matching the condition.


3. Use the pipe symbol and SQL for statistical analysis of the found raw data.
For example, calculate the distribution of log sources.

>?
> - For more information on the search and analysis syntax, see [Overview and Syntax Rules](https://intl.cloud.tencent.com/document/product/614/37803).
> - `__SOURCE__` is a system preset field indicating the source IP of a log. After [structuring](https://intl.cloud.tencent.com/document/product/614/31652) a log and enabling statistics in [**Key-Value Index**](https://intl.cloud.tencent.com/document/product/614/39594#.E9.94.AE.E5.80.BC.E7.B4.A2.E5.BC.95) for log fields, you can perform statistical analysis on log fields, such as log count by URL.
> 


## Additional Information

- [Concepts](https://www.tencentcloud.com/document/product/614/32848): This document describes the basic concepts of CLS, including log topic, logset, index, and segment.
- [Collecting and Searching NGINX Access Logs](https://intl.cloud.tencent.com/document/product/614/32939): This document describes how to collect NGINX logs and use regex to segment and extract log fields.
- [Migrating Local Logs Searched by the grep Command to CLS](https://intl.cloud.tencent.com/document/product/614/43571): This document describes how to convert the grep command to the CLS search syntax to quickly understand CLS syntax rules.
- [Tencent Cloud Service Log Access](https://intl.cloud.tencent.com/document/product/614/38200): CLS has integrated some commonly used Tencent Cloud products to easily collect their logs.
- [Creating Processing Task](https://intl.cloud.tencent.com/document/product/614/43568): The data processing feature provides the capabilities to filter, cleanse, mask, enrich, and distribute raw logs.
- [Monitoring Alarm Overview](https://intl.cloud.tencent.com/document/product/614/39573): An alarm policy can be set for logs, for example, triggering an alarm when the number of error logs exceeds 10 within one minute.

