## Overview
You can view the function execution logs in the SCF Console. You can filter to display real-time logs or logs from the last 24 hours. You can also specify a custom time range. You can choose to view all logs, or logs of successful, failed, timed-out, and excessive invocations and code exceptions via the SCF console.

## Directions
You can view function logs in the SCF Console.

### Viewing execution logs in the console
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. Click a function name to enter the function details page.
3. On the function details page, select **Log Query** on the left to open the **Invocation Logs** page:
![](https://main.qcloudimg.com/raw/75c09a3f4b6ba05fbebf8e96dd087bef.png)

### Finding an execution log
Follow the steps below to find an execution log as needed.

#### Invocation log
- In the top-right corner search box, enter the `requestID` of the execution log you want to view and press Enter:
![](https://main.qcloudimg.com/raw/9a56eb22b4a1fa2a94cc1e12d69640ce.png)
- You can also set custom search criteria in the top-left corner based on actual needs.
 - **All Logs**: you can select successful or failed invocations logs.
 - **Select a date**: you can view the execution logs generated in the last 20 days, including today. Currently, you can only search for logs within a 24-hour range.
 - **Real-time**: you can view the current execution log of a function.
 - **Last 24 hours**: you can view the execution logs generated in the previous 24 hours.


#### Advanced search
You can search for SCF logs by keyword or use query syntax to combine keywords for search. For more information, please see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/34382).

