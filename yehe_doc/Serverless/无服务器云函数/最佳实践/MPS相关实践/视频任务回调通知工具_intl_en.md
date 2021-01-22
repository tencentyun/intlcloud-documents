## Overview


This document describes how to use SCF to push [MPS](https://intl.cloud.tencent.com/document/product/1041) callback information. SCF is mainly used to process callback information, while MPS is mainly used for video processing tasks.


## Directions

<span id="step01"></span>

### Creating function

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Function Service** page, select the **Beijing** region and click **Create** to enter the function creation page and configure the following parameters:
 - **Function name**: enter "MPSWebHook".
 - **Runtime environment**: select "Nodejs 8.9".
 - **Creation method**: select **Function Template**.
 - **Fuzzy search**: enter "MPSWebhookDemo" and search.
>?Click **Learn More** in the template to view or download relevant information in the **Template Details** pop-up window.
3. After configuring the basic information, click **Next** to enter the function configuration page.
4. Keep the default function configuration and click **Complete**.

<span id="step02"></span>

### Configuring MPS trigger


1. After completing the [Creating function](#step01) step above, you will be redirected to the function management page by default.
2. On the left sidebar, select **Trigger Management** to enter the **Trigger Management** page.
3. Click **Create a Trigger** and add the created MPS trigger in the **Create a Trigger** pop-up window.
The main parameter information is as follows. Keep the remaining configuration items as default:

	- **Event type**: an MPS trigger pushes events in the account-level event type. Currently, two event types are supported: workflow task (`WorkflowTask`) and video editing task (`EditMediaTask`).
	- **Event processing**: an MPS trigger uses events generated at the service level as the event source, regardless of attributes such as region and resources. Only one single function can be bound to each event type for each account. If you need multiple functions to handle a task, please see [SDK for Node.js](https://intl.cloud.tencent.com/document/product/583/32747).
	>?When creating an MPS trigger for the first time, you need to click **SCF_QcsRole** and **MPS_QcsRole** to authorize the relevant service role.

<span id="step05"></span>

### Testing function
1. Log in to the [MPS console](https://console.cloud.tencent.com/mps) and execute a video processing workflow.
2. On the **[Function Service](https://console.cloud.tencent.com/scf/list)** page in the SCF console, click the name of the function created in the [Creating function](#step01) step above to enter the function details page.
3. Select the **Log Query** tab on the function details page to view the printed log information.
4. Switch to **WeCom** to view the callback notification result.
>?You can write specific data processing methods as needed.
