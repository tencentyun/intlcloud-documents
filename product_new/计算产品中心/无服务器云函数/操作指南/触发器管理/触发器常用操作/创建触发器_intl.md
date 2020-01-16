After created, you can create a trigger to associate a function with an event source. The associated event source will trigger the function synchronously or asynchronously as specified when an event is generated, and the event will be passed to the entry function as an input parameter upon triggering.

A function trigger can be created in the console or through TCCLI.

## Creating a Trigger in the Console

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select **Functions** on the left.
2. In the "Service" column at the top, select a region to view all the functions in it.
3. The function list includes the function name, monitoring information, function runtime environment, creation time, and modification time.
4. You can enter the details page of a function by clicking the function name, where lists the function configuration, function code, triggers, logs and monitoring information tabs.
5. Select the "Triggers" tab and click **Add a trigger**.
6. In the "Add a trigger" form, you can choose a trigger in the trigger drop-down menu. Different trigger types require different contents.
For a scheduled trigger, you need to enter the trigger name, cycle, and enablement for a timer trigger. For a COS trigger, you need to enter COS bucket, event type, and prefix/suffix filters.
> For more information on what to enter for specific triggers, see the applicable document.
7. After complete the configuration, click **Save** to create the trigger.
>To cancel the creation process, click **Cancel**.


## Creating a Trigger Through TCCLI

Before starting, you need to install and configure TCCLI by following the instructions in [TCCLI Installation and Configuration](https://intl.cloud.tencent.com/document/product/1013/33463).
Use the `tccli scf CreateTrigger` command to create a function trigger.
The sample below creates a timer trigger using TCCLI:

```
$ tccli scf CreateTrigger --FunctionName eventprint --TriggerName timer --Type timer --TriggerDesc '*/1 * * * *'
{
    "RequestId": "d86a6331-5aad-466a-9842-caffd7ba4bb8"
}
```

## Version and Trigger

A trigger can be created on a specified version of a function. An event of the trigger created in this manner will trigger the code of the specified version. 

When creating such a trigger in the console, you can switch to the desired version by choosing it in the version list at the upper right corner of the function interface, and then create the trigger on the triggers tab; when creating through TCCLI, you can specify the desired version on which to create the trigger by including a version number parameter.

>There are certain quota limits for the total number of triggers and number of triggers in each type for a function. Based on the function configuration, triggers created on different versions take up the quota of the function. To increase the trigger limits, please [contact us](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1).
