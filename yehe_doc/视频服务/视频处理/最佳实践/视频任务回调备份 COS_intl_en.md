## Overview
Backing up callbacks of MPS tasks to COS via SCF is a standard practice. MPS has a template in SCF which you can use to enable the feature. MPS executes video processing tasks; SCF handles callback messages, and COS provides permanent terminal storage.

## Directions
### Step 1. Create a function
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list), and click **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
![](https://main.qcloudimg.com/raw/29cd2fc9d699ac2af763749c2e67a472.png)
2. At the top of the **Function Service** page, select **Beijing** and click **Create** to enter the function creating page.
3. Set the following parameters:
	- **Function name**: enter a name, e.g., `MPSAnalysis`.
	- **Runtime**: message dump templates support only Python 2.7 at the moment.
	- **Create Method**: select **Function Template**.
	- **Fuzzy search**: enter **CLSSCFCOS** and search.
![](https://main.qcloudimg.com/raw/c9accdd429f7f1616020caa38d4f6c5e.png)
>? Click **Learn More** in the template to view details in the **Template Details** window, which can be downloaded.
4. Click **Next** to go to the function configuration page.
![](https://main.qcloudimg.com/raw/2342b403d79e55bca50c39b28fdcd634.png)
5. Keep the default configuration and click **Finish** to complete the creation.

### Step 2. Configure an MPS trigger
1. In the **[SCF console](https://console.cloud.tencent.com/scf), click **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar, and click the function created to go to the details page.
![](https://main.qcloudimg.com/raw/ac998f631557ea2214d66c2be9faaf5a.png)
2. Click **Trigger Management** > **Create a Trigger**. A trigger creation window pops up. Select **MPS trigger** for the trigger method.
![](https://main.qcloudimg.com/raw/e067ef8e3e09c07b723d041193b66c62.png)
The information of the main parameters is as follows. Keep the default settings for other parameters.
	> - **Event Type**: an MPS trigger pushes events at the account level. Two types of trigger events are supported now: Workflow Task (`WorkflowTask`) and Video Edit Task (`EditMediaTask`).
	>?
	> - A service role exception message will appear when you create an MPS trigger for the first time. Click **SCF_QcsRole** and **MPS_QcsRole** as prompted to grant the necessary permissions.
	>![](https://main.qcloudimg.com/raw/e6a5802db5fe9e054c2c50020f0403b1.png)
	> - An MPS trigger uses events generated at the service level as event sources, regardless of attributes such as region and resources. Each event type can be bound to only one function for each account. If you need multiple functions to handle a task, please see [Node.js SDK](https://intl.cloud.tencent.com/document/product/583/32747).
3. Click **Submit** to complete the configuration.
![](https://main.qcloudimg.com/raw/6a7d7009e36538491683173553b809fd.png)


### Step 3. Test the function
1. Start an MPS video processing workflow in the **[MPS console](https://console.cloud.tencent.com/mps)**.
2. Go to the **[SCF console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default)** to view the execution result.
Select the **Log Query** tab on the function details page to view the printed log information.
![](https://main.qcloudimg.com/raw/f5d10848b674f137826689ac1dc28c8a.png)
3. Log in to the [COS console](https://console.cloud.tencent.com/cos5) to view the data dumping and processing result.

>?You can write your own data processing methods as needed.
