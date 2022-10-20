After creating a function, you can create a trigger to associate the function with an event source. The associated event source will trigger the function synchronously or asynchronously as specified when an event is generated, and the event will be passed to the entry function as an input parameter upon triggering.

A function trigger can be created in the console or through Serverless Framework CLI.

>! Only API Gateway triggers can be created for HTTP-triggered functions. For more information, please see [Creating HTTP-Triggered Function](https://intl.cloud.tencent.com/zh/document/product/583/40689).

## Creating Trigger in Console

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Function Service** page, select the region and namespace where the function for which to create a trigger resides as shown below: 
![](https://main.qcloudimg.com/raw/e48bbf014e8c15fe22622fda5e2b8ffc.png)
The function list contains the function name, monitoring information, runtime environment, creation time, and modification time.
3. Click the function name to enter the function details page. 
The function details page contains the function management, trigger management, monitoring information, log query, and concurrency quota tabs:
4. On the function details page, select **Trigger Management** on the left to enter the trigger browsing and operation page. Click **Create a Trigger** to create a trigger as shown below:
![](https://main.qcloudimg.com/raw/89740ff73c89c3baa18ba995c86f3c0d.png)
5. In the **Create a Trigger** pop-up window, you can select different trigger methods in **Trigger Method**. The information to be entered varies by trigger method. 
For example, for a timer trigger, you need to enter the trigger name, cycle, and status. For a COS trigger, you need to enter the COS bucket, event type, and prefix/suffix filters.
>? For more information on what to enter for specific triggers, please see the applicable documents of [triggers](https://intl.cloud.tencent.com/document/product/583/9705).

7. After completing the trigger configuration, click **Submit** to create the trigger.
>? To cancel the creation process, click **Close**.





## Creating Trigger Through Serverless Framework CLI
>?Before starting, please install the Serverless Framework CLI tool first as instructed in [Installing Serverless Framework](https://intl.cloud.tencent.com/document/product/583/36263).
>
For local functions, please add the trigger description in the `serverless.yml` file. Then, run the `sls deploy` command on Serverless Framework CLI to add a trigger to the function.


## Version and Trigger

A trigger can be created on a specified version of a function. An event of the trigger created in this manner will trigger the code on the specified version.

When creating such a trigger in the console, you can switch to the desired version by choosing it in the version list in the top-right corner on the function page and then create the trigger on the "Triggers" tab.

>! There are certain quota limits for the total number of triggers and number of triggers in each type for a function. Based on the function configuration, triggers created on different versions take up the quota of the function. To increase the limit, please [contact us](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) for application.


