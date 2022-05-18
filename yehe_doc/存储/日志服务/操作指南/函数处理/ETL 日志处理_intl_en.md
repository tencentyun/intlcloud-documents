## Overview

This document describes how to use [SCF](https://intl.cloud.tencent.com/document/product/583) to process CLS logs. CLS is mainly used for log collection, while SCF mainly provides node computing capabilities.
The data flow is as follows:
![](https://main.qcloudimg.com/raw/3ad4864b402c547f8d7ba76746a1380f.png)

## Prerequisites
You have logged in to the [CLS console](https://console.cloud.tencent.com/cls).

## Directions

<span id="step02"></span>

### Creating log topic

Create two log topics as instructed in [Managing Log Topic](https://intl.cloud.tencent.com/document/product/614/34239).

>? As both the source and destination of data ETL are CLS, you need to create at least two topics.
>

<span id="step03"></span>

### Creating SCF function

Create a function as instructed in [Creating and Testing Function](https://intl.cloud.tencent.com/document/product/583/40689).
The main parameters are as follows:
 - Region: Select the **Beijing** region.
 - **Function Name**: Enter "CLSdemo".
 - **Creation Method**: Click **Template** and select the **CLSLogETL** template.

> ! You should select the VPC and subnet of CLS for the created function on the **Function Configuration** page.

<span id="step04"></span>

### Configuring CLS trigger

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Log Topic** to enter the log topic management page.
3. Find the log topic you just created and click its ID/name to enter the log topic details page.
4. On the log topic details page, select the **Function Processing** tab and click **Create**.
5. In the **Function Processing** pop-up window, add the created function and click **OK**.
The main parameter information is as follows. Use the default values for the remaining configuration items.
	- **Namespace**: Select the function namespace.
	- **Function Name**: Select the function created in the [Creating SCF function](#step03) step.
	- **Alias**: Select a function alias.
	- **Batch Window**: Configure the longest waiting time for a single event pull. Default value: 60s.

<span id="step05"></span>

### Testing function

1. Download the log file in the [test sample](https://main.qcloudimg.com/raw/6e0d4837eefd0ce77dac8a3973acdf39.zip), extract `demo-scf1.txt`, and import it to the source CLS service.
2. Switch to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default) to view the execution result.
   On the function details page, select the **Log Query** tab to view the printed log information.
   
3. Switch to the target CLS service to view the data processing result.
>? You can write specific data processing methods as needed.
> 
