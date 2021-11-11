## Overview

This document describes how to use SCF to dump CLS logs to ES. CLS is mainly used for log collection, while SCF mainly provides node computing capabilities for data processing. For the data processing flowchart, please see [Function Processing Overview](https://intl.cloud.tencent.com/document/product/614/38883).

## Directions

[](id:step01)

### Creating logset and topic

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Log Topic** on the left sidebar.
2. On the logset management page, select the region of the logset at the top.
3. Click **Create Log Topic** and enter relevant information in the **Create Logset** pop-up window:
   - Log Topic Name: enter `project_test` for example.
   - Logset Name: enter `nginx` for example.
   ![](https://qcloudimg.tencent-cloud.cn/raw/88ab08b439733ee2f2106d7a42ef1050.png)
4. Click **OK**.
5. The log topic is successfully added, and you will be redirected to the log topic management page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7fac2e633e9232428f78805abc06de4c.png)

[](id:step03)
### Creating SCF function

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Function Service** page, select the **Beijing** region and click **Create** to enter the function creation page and configure the following parameters:
  - **Creation method**: select **Template**.
  - **Fuzzy search**: enter "CLSToElasticsearch" and search.
3. Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded.
    ![](https://qcloudimg.tencent-cloud.cn/raw/41c42c5a4878ecfa98448fafa2a843f2.png)
4. After configuring the basic information, click **Next** to enter the function configuration page.
   - **Function name**: enter "CLSdemo".
5. Keep the default function configuration and click **Complete** to complete the function creation.
> ! You should select the same VPC and subnet of ES for the created function on the "Function Configuration" page as shown below:
>  ![](https://qcloudimg.tencent-cloud.cn/raw/cf2842d1c7bf83a9da1a21970fe58cf7.png)

[](id:step04)

### Configuring CLS trigger

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Logset** on the left sidebar.
2. Find the created logset and click **View** in the **Operation** column on the right to enter the logset details page.
3. On the log topic details page, select **Function Processing** and click **Create**. Add the created function in the pop-up "Function Processing" window as shown below:
	![](https://qcloudimg.tencent-cloud.cn/raw/64cc995a992fd3feb28098b3df95415d.png)
	The main parameter information is as follows. Keep the remaining configuration items as default:
	- **Namespace**: select the function namespace.
	- **Function name**: select the function created in the [Creating SCF function](#step03) step.
	- **Alias**: select a function alias.
	- **Maximum waiting time**: configure the longest waiting time for a single event pull. Default value: 60s.


[](id:step05)

### Testing function

1. Download the log file in the [test sample](https://main.qcloudimg.com/raw/6e0d4837eefd0ce77dac8a3973acdf39.zip), extract `demo-scf1.txt`, and import it to the source CLS service.
2. Switch to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default) to view the execution result.
   Select the **Log Query** tab on the function details page to view the printed log information as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/cc62580647a5828df530c9c95358dfe6.png)
3. Log in to the [ES console](https://console.cloud.tencent.com/es) to view the data dumping and processing result.
> ?You can write specific data processing methods as needed.
