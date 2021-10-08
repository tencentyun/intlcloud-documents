## Overview

This document describes how to use [SCF](https://intl.cloud.tencent.com/document/product/583) to process CLS logs. CLS is mainly used for log collection, while SCF mainly provides node computing capabilities for data processing.
The data flow is as follows:
![](https://main.qcloudimg.com/raw/71dc3d682daa5debfea9a9e715a0c974.svg)

## Directions

[](id:step01)
### Creating logset and topic
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Log Topic** on the left sidebar.
2. On the logset management page, select the region of the logset at the top.
3. Click **Create Log Topic** and enter relevant information in the **Create Logset** pop-up window:
      - Log Topic Name: enter `project_test` for example.
      - Logset Name: enter `nginx` for example.
     
4. Click **OK**.
5. The log topic is successfully added, and you will be redirected to the log topic management 

>? As both the source and destination of data ETL are CLS, you need to create at least two topics.

[](id:step03)

### Creating SCF function

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Function Service** page, select the **Beijing** region and click **Create** to enter the function creation page and configure the following parameters:
	- **Function name**: enter "CLSdemo".
	- **Runtime environment**: select **Python 2.7**.
	- **Creation method**: select **Function Template**.
	- **Fuzzy search**: enter "CLSLogETL" and search.
3. Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded.
4. After configuring the basic information, click **Next** to enter the function configuration page.
5. Keep the default function configuration and click **Complete** to complete the function creation.


[](id:step04)

### Configuring CLS trigger

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. At the top of the **Function Service** page, select the region and namespace where the function for which to configure a CLS trigger resides.
3. Click the function name to enter the function details page.
4. On the function details page, select **Trigger Management** on the left to enter the trigger browsing and operation page. Click **Create a Trigger** to create a trigger.
5. Add the created function in the **Create a Trigger** pop-up window 
6. After completing the trigger configuration, click **Submit** to create the trigger.

[](id:step05)

### Testing function

1. Download the log file in the [test sample](https://main.qcloudimg.com/raw/6e0d4837eefd0ce77dac8a3973acdf39.zip), extract `demo-scf1.txt`, and import it to the source CLS service.
2. Switch to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default) to view the execution result.
   Select the **Log Query** tab on the function details page to view the printed log information 
3. Switch to the target CLS service to view the data processing result.
> ?You can write specific data processing methods as needed.
