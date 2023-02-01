After creating a function, you can create a trigger to associate the function with an event source. The associated event source will trigger the function synchronously or asynchronously as specified when an event is generated, and the event will be passed to the entry function as an input parameter upon triggering.

A function trigger can be created in the console or on Serverless Cloud Framework CLI.

>! Only API Gateway triggers can be created for HTTP-triggered functions. For more information, see [Creating and Testing Function](https://intl.cloud.tencent.com/document/product/583/40689).

## Creating a Trigger in the Console

1. Log in to the SCF console and select **[Functions](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Functions** page, select the region and namespace where the function resides as shown below: 
![](https://main.qcloudimg.com/raw/e48bbf014e8c15fe22622fda5e2b8ffc.png)
3. Click the function name to enter the function details page.
4. Select **Trigger management** on the left to enter the trigger browsing and operation page. Click **Create trigger** to create a trigger as shown below: 
![](https://main.qcloudimg.com/raw/89740ff73c89c3baa18ba995c86f3c0d.png)
5. In the **Create trigger** pop-up window, select the trigger alias/version and trigger method as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/iQ77045_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219115801.png)
	- Trigger alias/version: Switch to the desired trigger version. A trigger can be created on a specified version of a function. An event of the trigger created in this manner will trigger the code on the specified version. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/583/35953).
	>! There are certain quota limits for the total number of triggers and number of triggers in each type for a function. Triggers created on different versions take up the quota of the function. To increase the limit, [contact us](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) for application.
	>
	
	- Trigger method: The information to be entered varies by trigger method. For example, for a timer trigger, you need to enter the trigger name, cycle, and status. For a COS trigger, you need to enter the COS bucket, event type, and prefix/suffix filters. For more information, see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).
7. After completing the trigger configuration, click **Submit** to create the trigger.






## Creating Trigger on Serverless Cloud Framework CLI
>?Before starting, install the Serverless Cloud Framework CLI tool first as instructed in [Installation](https://intl.cloud.tencent.com/document/product/583/36263).
>
For local functions, add the trigger description in the `serverless.yml` file. Then, run the `scf deploy` command on Serverless Cloud Framework CLI to add a trigger to the function.

 

