You can call the [created hello-world function](https://cloud.tencent.com/document/product/583/9204) using the test template provided by the console as follows.
1. On the details page of the created hello-world function, select the **Function code** tab.
2. On the "Function code" tab, click **Test** to execute the code and return the test result. See the figure below:
![](https://main.qcloudimg.com/raw/58cf73af5339844e9a6611412c3d4198.png)
>? 
> - You can also switch to the **Running log** tab to view the execution result.
> - If you need to change the test template or its content, you can do so by clicking **Change** or **Configure** respectively.
> - Different test templates simulate different trigger message sources, and the messages passed between different triggers and SCF are agreed upon data structures. For details, see [Overview of Triggers](https://cloud.tencent.com/document/product/583/9705).

3. Switch to the **Monitoring information** tab to view the monitoring information.
>! The minimal granularity of monitoring statistics collection is 1 minute. You need to wait for 1 minute before you can view the current monitoring record.

During this test, SCF will get the data structures of the "Hello world event template" in the `event` parameter of the `main_handler`.
```
{
  "key1": "test value 1",
  "key2": "test value 2"
}
```

