## Overview

This document describes how to use SCF to dump CLS logs to CKafka. CLS is mainly used for log collection, SCF mainly provides node computing capabilities for data processing, and CKafka mainly provides terminal dumping capabilities for data streams. For the data processing flowchart, please see [Function Processing Overview](https://intl.cloud.tencent.com/document/product/614/38883).



## Directions

[](id:step01)

### Creating logset and topic
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls), and click **Log Topic** on the left sidebar.
2. On the logset management page, select the logset region at the top.
3. Click **Create Log Topic** and enter relevant information in the **Create Logset** pop-up window:
  - Log Topic Name: enter `project_test` for example.
  - Logset Name: enter `nginx` for example.

4. Click **OK**.
5. Once the log topic is added successfully, you will be directed to the logset management page. See the figure below.




[](id:step03)

### Creating an SCF function

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Function Service** page, select the **Beijing** region and click **Create** to go to the function creating page and configure the following parameters:
 - **Function name**: enter **CLSdemo**.
 - **Runtime environment**: select **Python 2.7**.
 - **Creation Method**: select **Function Template**.
 - **Fuzzy search**: enter **CLSToCkafka** and search.
3. Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded.

4. After configuring the basic information, click **Next** to go to the function configuration page.
5. Keep the default configuration and click **Finish** to complete the function creation.
>! You should select the same VPC and subnet of CKafka for the created function on the **Function Configuration** page as shown below:



[](id:step04)

### Configuring CLS triggers
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls), and click **Log Topic** on the left sidebar.
2. Locate the existing logset you want, for example, **project_test**, and click **View** under **Operation** on the right to go to the logset details page.
3. On the log topic details page, select **Function Processing** and click **Create** in the top-right corner. Add the created function in the **Function Processing** pop-up window.

The main parameter information is as follows. Use the default values for the remaining configuration items.
 - **Namespace**: select the function namespace.
 - **Function Name**: select the function created in the [Creating SCF function](#step03) step.
 - **Alias**: select a function alias.
 - **Maximum waiting time**: configure the longest waiting time for a single event pull. Default value: 60s.

[](id:step05)

### Testing the function
1. Download the log file in the [test sample](https://main.qcloudimg.com/raw/6e0d4837eefd0ce77dac8a3973acdf39.zip), extract `demo-scf1.txt`, and import it to the source CLS service.
2. Switch to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default) to view the execution result.
Select the **Log Query** tab on the function details page to view the printed log information.

3. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka) to view the data dumping and processing result.
>?You can write your own data processing methods as needed.
