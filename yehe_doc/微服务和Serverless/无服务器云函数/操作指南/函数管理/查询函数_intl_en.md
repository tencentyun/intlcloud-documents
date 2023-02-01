A function can be queried in the console or on Serverless Cloud Framework CLI.

## Viewing a Function in the Console
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select **Functions** on the left sidebar.
2. Select the region and namespace for which to view functions at the top of the **Functions** page. In the function list, you can view all the functions in the specified region and namespace as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Azbs372_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219114446.png)
3. The function list displays the function name, monitoring information, function type, runtime environment, log configuration, and creation time. You can customize the displayed fields as needed by clicking ![](https://qcloudimg.tencent-cloud.cn/raw/0cb8ff5c087a438c195cd954e321754f.png) on the right as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EB2D161_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219114927.png)
In the pop-up window, select the fields you want to display and click **OK** as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/7ach916_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219115035.png)
3. Click the function name to enter the function details page as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/b2xD508_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219115137.png)
The function details page contains the following information:
	- **Function management**: View and manage the configurations, [codes](https://intl.cloud.tencent.com/document/product/583/39008), and [layers](https://intl.cloud.tencent.com/document/product/583/37039) of the function.
	- **Version management**: Fixate the code and configuration of the function by publishing a version. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/583/35953). 
	- **Alias management**: Use an alias to call the bound function. 
	- **Trigger management**: View the triggers configured for the function and create triggers. For more information, see [Creating Triggers](https://intl.cloud.tencent.com/document/product/583/31441). 
	- **Monitoring information**: View the monitoring information of function execution. For more information, see [Descriptions of monitoring metrics](https://intl.cloud.tencent.com/document/product/583/32739).
	- **Log query**: View the execution logs of the function and filter logs by certain criteria. For more information, see [Viewing Execution Logs](https://intl.cloud.tencent.com/document/product/583/32740).
	- **Concurrency quota**: View the concurrency quota of the function and set the reserved quota and provisioned concurrency of the function. For more information, see [Concurrency Overview](https://intl.cloud.tencent.com/document/product/583/37040).
	- **Deployment logs**: View the deployment logs of the function.


## Getting Deployment Information on Serverless Cloud Framework CLI
>?Before starting, install the Serverless Cloud Framework CLI tool first as instructed in [Installation](https://intl.cloud.tencent.com/document/product/583/36263).
>
You can run the `scf info` command on Serverless Cloud Framework CLI to view deployment information.

