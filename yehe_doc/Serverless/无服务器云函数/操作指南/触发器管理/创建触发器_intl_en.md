After creating a function, you can create a trigger to associate the function with an event source. The associated event source will trigger the function synchronously or asynchronously as specified when an event is generated, and the event will be passed to the entry function as an input parameter upon triggering.

A function trigger can be created in the console or through SCF CLI.

## Creating Trigger in Console

1. Log in to the SCF Console and select **[Functions](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the "Functions" page, select the region and namespace where the function for which to create a trigger resides.
The function list contains the function name, monitoring information, runtime environment, creation time, and modification time.
3. Click the function name to enter the function details page.
The function details page contains the function configuration, function code, triggers, logs, and monitoring tabs.
4. Select the **Triggers** tab to enter the trigger browsing and operation page. Click **Add Trigger** to create a trigger.
5. In the expanded "Add Trigger" form, you can select different trigger types in **Trigger Type**. The information to be entered varies by trigger type.
For example, for a timer trigger, you need to enter the trigger name, cycle, and status. For a COS trigger, you need to enter the COS bucket, event type, and prefix/suffix filters.
> For more information on what to enter for specific triggers, please see the applicable documents of [triggers](https://intl.cloud.tencent.com/document/product/583/9705).
7. After completing the configuration, click **Save** to create the trigger.
> To cancel the creation process, click **Cancel**.





## Creating Trigger Through SCF CLI
>Before starting, you need to install and configure SCF CLI as instructed in [CLI Installation and Configuration](https://intl.cloud.tencent.com/document/product/583/32754).
>
For local functions, please add the trigger description in the `template.yaml` file as instructed in [Event Source Types](<https://intl.cloud.tencent.com/document/product/583/32761>). Then, run the `scf deploy` command on SCF CLI to add a trigger to the function. For more information, please see [Package Deployment](<https://intl.cloud.tencent.com/document/product/583/32756>).

## Version and Trigger

A trigger can be created on a specified version of a function. An event of the trigger created in this manner will trigger the code on the specified version. 

When creating such a trigger in the console, you can switch to the desired version by choosing it in the version list in the top-right corner on the function page and then create the trigger on the "Triggers" tab.

> There are certain quota limits for the total number of triggers and number of triggers in each type for a function. Based on the function configuration, triggers created on different versions take up the quota of the function. To increase the limit, please [contact us](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) for application.
