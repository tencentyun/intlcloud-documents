Backing up callbacks of MPS tasks to COS via SCF is a standard practice. MPS has a template in SCF which you can use to enable the feature. MPS executes video processing tasks; SCF handles callback messages, and COS provides permanent terminal storage.

## Directions
### Step 1. Create a function
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list), and click **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
![](https://qcloudimg.tencent-cloud.cn/raw/d19e5af310ff9e75498bba4f7d63abc4.png)
2. At the top of the **Function Service** page, select **Beijing** and click **Create** to enter the function creating page.
3. Set the following parameters:
  - **Create Method**: select **Template**.
  - **Fuzzy search**: search **CLSSCFCOS**.
![](https://qcloudimg.tencent-cloud.cn/raw/8b25b3314ee4ad6040a888b48e0ab889.png)
>? You can click **Learn More** in a template to view its details or download the template.
4. Click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/daf1fa4f6c4bb4f402a3db5826b46c9a.png)
5. Keep the default configuration and click **Complete** to complete the creation.

### Step 2. Configure an MPS trigger
1. In the **[SCF console](https://console.cloud.tencent.com/scf)**, click **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar, and click the function created to go to the details page.
2. Click **Trigger Management** > **Create a Trigger**. A trigger creation window pops up. Select **MPS trigger** for the trigger method.

The main parameter information is as follows. Use the default values for the remaining configuration items.
  - **Event Type**: an MPS trigger pushes events at the account level. Two types of trigger events are supported now: Workflow Task (`WorkflowTask`) and Video Edit Task (`EditMediaTask`).
>?
>- A service role error message will appear when you create an MPS trigger for the first time. Click **SCF_QcsRole** and **MPS_QcsRole** to grant the necessary permissions as prompted.
- An MPS trigger uses events generated at the service level as event sources, regardless of attributes such as region and resources. Each event type can be bound to only one function for each account. If you need multiple functions to handle a task, please see [Node.js SDK](https://intl.cloud.tencent.com/document/product/583/32747).
3. Click **Submit** to complete the configuration.



### Step 3. Test the function
1. Start an MPS video processing workflow in the **[MPS console](https://console.cloud.tencent.com/mps)**.
2. Go to the **[SCF console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default)** to view the execution result.
Select the **Log Query** tab on the function details page to view the printed log information.
3. Log in to the [COS console](https://console.cloud.tencent.com/cos5) to view the data dumping and processing result.

>? You can write your own data processing methods as needed.
