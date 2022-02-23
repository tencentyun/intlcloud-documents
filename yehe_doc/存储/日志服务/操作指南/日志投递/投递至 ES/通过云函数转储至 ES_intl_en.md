## Overview

This document describes how to use SCF to dump CLS logs to ES. CLS is mainly used for log collection, and SCF mainly provides node computing capabilities for data processing. For the data processing flowchart, please see [Function Processing Overview](https://intl.cloud.tencent.com/document/product/614/38883).

## Directions

### Creating a log topic

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Log Topic** in the left sidebar.
3. On the log topic management page, select a region, click **Create Log Topic**.
4. In the pop-up, configure the following settings:

 - Log Topic Name: for example, enter `nginx`.
 - Partitions: the default value is 1. For details about topic partitions, see [Topic Partition](https://intl.cloud.tencent.com/document/product/614/33779). 
 - Partition Auto-Split: enabled by default.
 - Maximum Partitions: you can specify the maximum number of partitions. The value is up to 50.
 - Logset Operation:
    - Select an existing logset: select a target logset from the drop-down list of the **Logset**. The log retention period is determined by the logset retention period.
    - Create logset:
      - Logset Name: for example, enter `cls_test`
      - Log Retention Period: the default value is 30
5. Click **OK**.
After the log topic is created, you can click its ID/name on the “Log Topic” page to view its details.


>?
>- You’re advised to select the same region as the CVM or any other Tencent Cloud service from which you collect logs.
>- Once a logset is created, you cannot modify its region.
>- The logs can be retained for 1-366 days. To retain logs for longer, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>

### Creating SCF functions

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** in the left sidebar.
2. At the top of the **Function Service** page, select the **Beijing** region and click **Create** to enter the function creating page and configure the following parameters:
- **Function name**: enter **CLSdemo**.
- **Runtime environment**: select **Python 2.7**.
- **Creation method**: select **Function Template**.
- **Fuzzy search**: enter **CLSToElasticsearch** and search.
3. Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded.

4. After configuring the basic information, click **Next** to enter the function configuration page.
5. Keep the default configuration and click **Complete** to complete the function creation.
> ! You should select the same VPC and subnet of CLS for the created function on the **Function Configuration** page.
> 

### Configuring CLS triggers

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Logset** on the left sidebar.
2. Locate the existing logset you want, and click **View** under “Operation” on the right to enter the logset details page.
3. On the log topic details page, select **Function Processing** and click **Create**. Add the created function in the **Function Processing** pop-up window.
The main parameter information is as follows. Use the default values for the remaining configuration items.
- **Namespace**: select the function namespace.
- **Function name**: select the function created in the [Creating SCF function](#step03) step.
- **Alias**: select a function alias.
- **Maximum waiting time**: configure the longest waiting time for a single event pull. Default value: 60s.

### Testing the function

1. Download the log file in the [test sample](https://main.qcloudimg.com/raw/6e0d4837eefd0ce77dac8a3973acdf39.zip), extract `demo-scf1.txt`, and import it to the source CLS service.
2. Switch to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default) to view the execution result.
Select the **Log Query** tab on the function details page to view the printed log information.
3. Log in to the [ES console](https://console.cloud.tencent.com/es) to view the data dumping and processing result.
> ?You can write specific data processing methods as needed.
