After a video is processed by MPS, it’s a standard practice to send a notification that the video processing task is completed. MPS has a template in SCF which you can use to enable this feature.

## Use Cases
The example in this document uses MPS and SCF. MPS executes vide processing tasks, and SCF handles callback messages.

## Directions
### Step 1. Create a function
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list), and click **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.

2. At the top of the **Function Service** page, select the **Beijing** region and click **Create** to enter the function creating page.
3. Set the following parameters:
	- **Function name**: enter a name, e.g., MPSAnalysis.
	- **Runtime**: the task callback template supports only Nodejs 8.9 at the moment.
	- **Create Method**: select **Function Template**.
	- **Fuzzy search**: search "MPS Webhook template".

>? Click **Learn More** in the template to view details in the **Template Details** window, which can be downloaded.
4. Click **Next** to go to the function configuration page.

5. Keep the default configuration and click **Finish** to complete the creation.


### Step 2. Configure an MPS trigger
1. In the **[SCF console](https://console.cloud.tencent.com/scf), click **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar, and click the function created to go to the details page.

2. Click **Trigger Management** > **Create a Trigger**. A trigger creation window pops up. Select **MPS trigger** for the trigger method.

The information of the main parameters is as follows. Keep the default settings for other parameters.
	> - **Event Type**: an MPS trigger pushes events at the account level. Two types of trigger events are supported now: Workflow Task (`WorkflowTask`) and Video Edit Task (`EditMediaTask`).
	>?
	> - A service role exception message will appear when you create an MPS trigger for the first time. Click **SCF_QcsRole** and **MPS_QcsRole** as prompted to grant the necessary permissions.

	> - An MPS trigger uses events generated at the service level as event sources, regardless of attributes such as region and resources. Each event type can be bound to only one function for each account. If you need multiple functions to handle a task, please see [Node.js SDK](https://intl.cloud.tencent.com/document/product/583/32747).
3. Click **Submit** to complete the configuration.



### Step 3. Test the function
1. Log in to the [MPS console](https://console.cloud.tencent.com/mps) and start a video processing workflow.
2. Go to the **[SCF console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default)** to view the execution result.
Select the **Log Query** tab on the function details page to view the printed log information as shown below:

3. Log in to the [COS console](https://console.cloud.tencent.com/cos5) to view the data dumping and processing result.

>?You can write your own data processing methods as needed.
