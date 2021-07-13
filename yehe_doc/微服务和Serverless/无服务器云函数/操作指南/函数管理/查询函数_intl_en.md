A function can be queried in the console or on Serverless Framework CLI.

## Viewing Function in Console
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and select "Function Service" on the left sidebar.
2. Select the region for which to view functions at the top. In the function list, you can view all the functions in the specified region.
4. The list page includes the function name, monitoring information, function runtime environment, creation time, and modification time.
5. Click the function to enter the details page. It includes the following tabs:
 * Function Configuration: it displays the basic configuration of the function, including function name, runtime environment, configured memory, timeout period, function description, network configuration, and environment variable configuration information.
 * Function Code: it displays the editable function code, execution method, and function submission method. You can test run the function and modify function testing templates on this tab, which displays return values, logs, and execution information of the test runs.
 * Triggers: it displays the configured triggers for the function, and you can configure a trigger on this tab.
 * Logs: it displays the function execution logs, where you can filter logs by certain criteria for display.
 * Monitoring: it displays function execution monitoring information.

## Getting Function Information on SCF CLI
>Before starting, you need to install and configure SCF CLI as instructed in CLI Installation and Configuration.
>
You can run the `scf function list` command on SCF CLI to get the function list.
