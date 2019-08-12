
You need to create a logset and log topic to store and view the flow logs.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), and select **Products** -> **Cloud Compute & Network** -> **[Cloud Log Service](https://console.cloud.tencent.com/cls/logset)** -> **Logset Management**. 
2. Create a logset service. Note that **there is no need to enable the agent**.
![1](https://main.qcloudimg.com/raw/a73b4cf8b0a1cd0ea103a67f829ec789.png) 
3. After the logset service is created successfully, please enable **Index** to view and retrieve the flow logs.
![2](https://main.qcloudimg.com/raw/edf1d862751eb1c16f28fd1ee7dfb5cc.png)
![3](https://main.qcloudimg.com/raw/eee69cb13205e1d727948a71deb42c44.png)
![4](https://main.qcloudimg.com/raw/1e43e728dd4832c37d86cb054c8ae941.png)

>**Notes:** 
>- You **do not need to install agent**, nor do you need to be concerned about the status of the server group. 
>- If you don't need to deliver flow logs to services like [COS](https://cloud.tencent.com/document/product/436/6222), you **don't need to be concerned about delivery tasks**.




