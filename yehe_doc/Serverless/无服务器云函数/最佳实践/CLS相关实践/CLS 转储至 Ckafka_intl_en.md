## Overview

This document describes how to use SCF to dump CLS logs to CKafka. CLS is mainly used for log collection, SCF mainly provides node computing capabilities for data processing, and CKafka mainly provides terminal dumping capabilities for data streams. For the data processing flowchart, please see [Function Processing Overview](https://intl.cloud.tencent.com/document/product/614/38883).



## Directions

[](id:step01)

### Creating logset and topic
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Log Topic** on the left sidebar.
2. On the logset management page, select the region of the logset at the top.
3. Click **Create Log Topic** and enter relevant information in the **Create Logset** pop-up window:
  - Log Topic Name: enter `project_test` for example.
  - Logset Name: enter `nginx` for example.
![](https://qcloudimg.tencent-cloud.cn/raw/aef0c21a0ffb668c11ec0fe88b4c38f1.png)
4. Click **OK**.
5. The log topic is successfully added, and you will be redirected to the log topic management page as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/18a11bc00a7e328d19c827365ac01b68.png)



[](id:step03)

### Creating SCF function

1. Log in to the [Serverles](https://console.cloud.tencent.com/scf/list) console and enter the function service page.
2. At the top of the **Function Service** page, select the **Beijing** region and click **Create** to enter the function creation page and configure the following parameters:
 - **Function name**: enter "CLSdemo".
 - **Runtime environment**: select **Python 2.7**.
 - **Creation method**: select **Function Template**.
 - **Fuzzy search**: enter "CLSToCkafka" and search.
3. Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded.
4. After configuring the basic information, click **Next** to enter the function configuration page.
5. Keep the default function configuration and click **Complete** to complete the function creation.
> ! You should select the same VPC and subnet of CKafka for the created function on the "Function Configuration" page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/05447e52556ab3428cd51b4726b7ba5c.png)


[](id:step04)

### Configuring CLS trigger
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Log Topic** on the left sidebar.
2. Find the created logset (such as "project_test") and click **View** in the **Operation** column on the right to enter the logset details page.
3. On the log topic details page, select **Function Processing** and click **Create** in the top-right corner. Add the created function in the pop-up "Function Processing" window as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/00b7040c6699b366a368a01ba4270c5e.png)
The main parameter information is as follows. Keep the remaining configuration items as default:
 - **Namespace**: select the function namespace.
 - **Function name**: select the function created in the [Creating SCF function](#step03) step.
 - **Alias**: select a function alias.
 - **Maximum waiting time**: configure the longest waiting time for a single event pull. Default value: 60s.

[](id:step05)

### Testing function
1. Download the log file in the [test sample](https://main.qcloudimg.com/raw/6e0d4837eefd0ce77dac8a3973acdf39.zip), extract `demo-scf1.txt`, and import it to the source CLS service.
2. Switch to the [Serverless console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default) to view the execution result.
Select the **Log Query** tab on the function details page to view the printed log information as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/b9dc2dfda8658d1a21739a2898a41c15.png)
3. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka) to view the data dumping and processing result.
>?You can write specific data processing methods as needed.
