A function can be queried in the console or on Serverless Framework CLI.

## Viewing Function in Console
1. Log in to the [SCF](https://console.cloud.tencent.com/scf) console and select **Function Service** on the left sidebar.
2. Select the region and namespace for which to view functions at the top of the **Function Service** page. In the function list, you can view all the functions in the specified region and namespace. 
The list page includes information such as function name, monitoring information, function runtime environment, creation time, and modification time.
3. Click the function name to enter the function details page. 
The function details page contains the function management, trigger management, monitoring information, log query, and concurrency quota tabs:
 - **Function management tab**: you can view and manage function configuration, function code, function layer, function version and alias, function monitoring data, and log information.
 - **Trigger management tab**: it displays the configured triggers for the function, and you can create a trigger on this tab.
 - **Monitoring information tab**: it displays function execution monitoring information.
 - **Log query tab**: it displays the function execution logs, where you can filter logs by certain criteria for display.
 - **Concurrency quota tab**: it displays the concurrency quota of the function. You can set the maximum dedicated quota and provisioned concurrency of the function here.


## Getting Deployment Information on Serverless Framework CLI
>?Before starting, please install the Serverless Framework CLI tool first as instructed in [Installing Serverless Framework](https://intl.cloud.tencent.com/document/product/583/36263).
>
You can run the `sls info` command on Serverless Framework CLI to view deployment information.
