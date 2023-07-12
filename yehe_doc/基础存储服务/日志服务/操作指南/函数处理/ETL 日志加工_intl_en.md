## Overview

This document describes how to use [SCF](https://intl.cloud.tencent.com/document/product/583) to process CLS logs. CLS is mainly used for log collection, and SCF mainly provides node computing capabilities for data processing.
The data flow is as follows:

![](https://main.qcloudimg.com/raw/3ad4864b402c547f8d7ba76746a1380f.png)

## Directions

<span id="step01"></span>

### Creating logset

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Logset** on the left sidebar.
2. On the logset management page, select the region of the logset at the top.
3. Click **Create Logset** and enter relevant information in the **Create Logset** pop-up window:
4. Click **OK**.

<span id="step02"></span>

### Creating log topic

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Logset** on the left sidebar.
2. Find the created logset and click **View** in the **Operation** column on the right to enter the logset details page.
3. Click **Add Log Topic** and enter the following relevant information in the **Add Log Topic** window:
   - Log Topic Name: enter `nginx` for example.
   - Topic Partitions: for more information on topic partition, please see [Topic Partition](https://intl.cloud.tencent.com/document/product/614/33779). One partition is created by default.
4. Click **OK**.
5. The log topic is successfully added, and you will be redirected to the log topic management page.
>? As both the source and destination of data ETL are CLS, you need to create at least two topics.

<span id="step03"></span>

### Creating SCF function

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Function Service** page, select the **Beijing** region and click **Create** to enter the function creating page and configure the following parameters:
	- **Function name**: enter **CLSdemo**.
	- **Runtime environment**: select **Python 2.7**.
	- **Creation method**: select **Function Template**.
	- **Fuzzy search**: enter **CLSLogETL** and search.
3. Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded.
4. After configuring the basic information, click **Next** to enter the function configuration page.
5. Keep the default function configuration and click **Complete** to complete the function creation.
> ! You should select the same VPC and subnet of CLS for the created function on the **Function Configuration** page as shown below:


<span id="step04"></span>

#### Configuring CLS trigger

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Logset** on the left sidebar.
2. Find the created logset and click **View** in the **Operation** column on the right to enter the logset details page.
3. On the log topic details page, select **Function Processing** and click **Create**. Add the created function in the **Function Processing** pop-up window as shown below:
The main parameter information is as follows. Keep the remaining configuration items as default:
	- **Namespace**: select the function namespace.
	- **Function name**: select the function created in the [Creating SCF function](#step03) step.
	- **Alias**: select a function alias.
	- **Maximum waiting time**: configure the longest waiting time for a single event pull. Default value: 60s.

<span id="step05"></span>

### Testing function

1. Download the log file in the [test sample](https://main.qcloudimg.com/raw/6e0d4837eefd0ce77dac8a3973acdf39.zip), extract `demo-scf1.txt`, and import it to the source CLS service.
2. Switch to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default) to view the execution result.
   Select the **Log Query** tab on the function details page to view the printed log information as shown below:
3. Switch to the target CLS service to view the data processing result.
> ?You can write specific data processing methods as needed.
