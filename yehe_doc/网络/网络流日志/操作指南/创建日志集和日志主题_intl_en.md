You need to create logsets and log topics to store and view the flow logs.
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Logset** on the left sidebar to enter the **Logset Management** page. 
2. Select a desired region at the top of the page and click **Create Logset**.
3. In the pop-up window, enter the logset name, specify a retention period, and click **OK**.
![](https://main.qcloudimg.com/raw/c327687599503f2343c245146aee645d.png)
4. Click **create log topic** in the **Logset created successfully** window that pops up.
5. On the details page of the logset, click **Add Log Topic**.
6. In the pop-up window, enter log topic name and partition, and click **OK**.
>?After the auto-split feature is enabled, the partition will be automatically split up to 50 partitions based on the actual write capacity when the write requests or write traffic of the partition always exceed the capability.
If the log topic has the maximum number of partitions, split will not be triggered. Excessive partitions will be rejected by returning an [error code](https://intl.cloud.tencent.com/document/product/614/12402).
>
![](https://main.qcloudimg.com/raw/2b9471be51ef400df3fb21b7ae4b02b5.png)
7. On the details page of the log topic, select the **Index Configuration** tab and click **Edit** in the top-right corner.
![](https://main.qcloudimg.com/raw/d79050aed976e6207844013babf81f22.png)
8. Enable the index and click **Save**. Now you can view and search for flow logs.
>?
>- You do not need to install agents or care about the server group status. 
>- If you do not need to upload flow logs to services such as [COS](https://intl.cloud.tencent.com/document/product/436/6222), ignore shipping task.
>
![](https://main.qcloudimg.com/raw/c916eeb3d27f55f335bf9c0ec0098b10.png)
