## Operation Scenarios
When Serverless Cloud Function (SCF) is used for function computation, a large number of function execution logs will be generated. Such logs have been connected to the Tencent Cloud Log Service (CLS), which can collect logs in real time. You can perform various operations such as real-time log search, delivery, and consumption on the CLS platform as shown below:
![](https://main.qcloudimg.com/raw/ca4e6aefa5b78812d98ea8baaac25238.png)


## Prerequisites
Before using the SCF real-time log service, you need to activate [CLS](https://intl.cloud.tencent.com/product/cls) first.


## Directions
### Creating logsets and log topics
Log in to the [CLS Console](https://console.cloud.tencent.com/cls) and [create a logset and log topic](https://intl.cloud.tencent.com/document/product/614/31592). This document uses the creation of the `SCF-test` log set and log topic in Guangzhou as an example.
>For the logset region, please select the region where the SCF service is located. Cross-region log push is not supported currently.
>

### Configuring CLS
1. Log in to the SCF Console and select **[Functions](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. Select the SCF region and namespace at the top of the page and click the function name in the list for which to collect logs in real time.
3. On the "Function Configuration" page, click **Edit** in the top-right corner.
4. In "Log Delivery", select the logset and log topic already created for this function. This document uses `SCF-test` as an example.
5. Click **Save** to connect to the CLS platform.

### Enabling index
>If you want to use the log search feature, you need to enable the index manually as instructed below:
>
1. Log in to the CLS Console and select **[Log Sets](https://console.cloud.tencent.com/cls/logset)** on the left sidebar.
2. Click the ID of a created logset to enter the "Basic Info" page.
3. Select **Manage** to the right of the log topic row to enter the "Basic Info" page of the log topic.
4. On the "Basic Info" page of the log topic, click **Index Configuration**.
5. Click **Edit** in the top-right corner to enable the index and save the change.
For more information on other features such as real-time log search, delivery, and consumption, please see the [CLS documentation](https://intl.cloud.tencent.com/document/product/614). These features can be used in the [CLS Console](https://console.cloud.tencent.com/cls) directly.


### Example of real-time search
>Before using the real-time search feature, please make sure that your SCF log service has been connected to the CLS platform and the index has been enabled for the log topic to be searched.
>
1. Log in to the CLS Console and select **[Log Search](https://console.cloud.tencent.com/cls/search)** on the left sidebar.
2. On the "Search and Analysis" page, select the desired log topic and time and enter the search syntax in the input box. This document uses `START` as an example.
The search syntax supports keyword search, fuzzy search, range search, and other search methods. For more information, please see [Syntax Rules](https://intl.cloud.tencent.com/document/product/614/16981).
3. Click **Query and Analyze** to view real-time log information.
