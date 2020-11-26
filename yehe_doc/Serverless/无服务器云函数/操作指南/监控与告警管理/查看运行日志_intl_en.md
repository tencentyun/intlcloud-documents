## Overview
You can view the execution logs of functions in the SCF Console. Specifically, you can search for logs in the specified time range and view logs in real time or from the last 24 hours. Currently, the console allows you to view all logs as well as logs of successful, failed, timed-out, and excessive invocations and code exceptions.

## Directions
You can view function logs in the SCF Console.

### Viewing execution logs in console
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. Click a function name to enter the function details page.
3. On the function details page, select **Log Query** on the left to open the function's **Invocation Logs** page as shown below:
![](https://main.qcloudimg.com/raw/75c09a3f4b6ba05fbebf8e96dd087bef.png)

### Finding execution log
You can find an execution log as needed:

#### Invocation log
- Enter the `requestID` of the execution log to be viewed in the search box in the top-right corner and press Enter to view it as shown below:
![](https://main.qcloudimg.com/raw/9a56eb22b4a1fa2a94cc1e12d69640ce.png)
- Set custom search criteria in the top-left corner based on your actual needs to view the desired executions logs.
 - **All Logs**: you can select logs of successful invocations or failed invocations.
 - **Select a date**: you can view the execution logs generated in the last 20 days up to today. Currently, you can only search for logs in a time range of no more than 24 hours.
 - **Realtime**: you can view the current execution log of a function.
 - **Last 24 hours**: you can view the execution logs generated in the last 24 hours.


#### Advanced search
You can search for SCF logs by keyword or use query syntax to combine keywords for search. For more information, please see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/34382).

