## Overview
When SCF is used for function computation, a large number of function execution logs will be generated. You can view and search for logs generated in the last 15 days in the [SCF Console](https://console.cloud.tencent.com/scf/index?rid=1).
If you need to store, deliver, or consume logs in a persistent manner and monitor and set alarms on log content, you can deliver logs to the Tencent Cloud Log Service (CLS) platform as shown below:
![](https://main.qcloudimg.com/raw/ca4e6aefa5b78812d98ea8baaac25238.png)


## Prerequisites
Before using the SCF real-time log service, you need to activate [CLS](https://intl.cloud.tencent.com/product/cls) first.
## Directions
### Creating logset and log topic
Log in to the [CLS Console](https://console.cloud.tencent.com/cls) and [create a logset and log topic](https://intl.cloud.tencent.com/document/product/614/31592). This document uses the creation of the `SCF-test` log set and log topic in Guangzhou as an example as shown below:
>!For the logset region, please select the region where the SCF service is located. Cross-region log push is not supported currently.
>
![](https://main.qcloudimg.com/raw/372b2b2c57ca6f22181d923889f7d8ca.png)

### Configuring CLS
1. Log in to the SCF Console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. Select the SCF region and namespace at the top of the page and click the function name in the list for which to collect logs in real time.
3. On the "Function configuration" page, click **Edit** in the top-right corner as shown below:
![](https://main.qcloudimg.com/raw/6b74418e46923017c70cdd7a829d650d.png)
4. In "Log Delivery", click "Enable" and select the logset and log topic already created for this function. This document uses `SCF-test` as an example as shown below:
![](https://main.qcloudimg.com/raw/3a51957107ea5152ce9f17c66cda461d.png)
5. Click **Save** to connect to the CLS platform.

### Enabling index
>? Log retrieval depends on the index configuration of the log topic. Please enable the index as instructed below:
>
1. Log in to the CLS Console and select **[Log Sets](https://console.cloud.tencent.com/cls/logset)** on the left sidebar.
2. Click the ID of a created logset to enter the "Basic Info" page.
3. Select **Manage** to the right of the log topic row to enter the "Basic Info" page of the log topic.
4. On the "Basic Info" page of the log topic, click **Index Configuration** as shown below:
![](https://main.qcloudimg.com/raw/49bd80b80664830aac2f03a0b444bbb8.png)
4. Click **Edit** in the top-right corner, enable "Key-Value Index", and add "Field Name" and "Field Type" according to the following table.
 >? For functions configured with CLS, to ensure the display effect of the logs in the SCF Console, please toggle on "Enable Statistics" for the field in the key-value index configuration as shown below:
![](https://main.qcloudimg.com/raw/989273eed3d2405f59cc35ff648b8422.png)
<table>
<thead>
<tr>
<th>Field Name</th>
<th>Field Type</th>
</tr>
</thead>
<tbody><tr>
<td>SCF_FunctionName</td>
<td>text</td>
</tr>
<tr>
<td>SCF_Namespace</td>
<td>text</td>
</tr>
<tr>
<td>SCF_StartTime</td>
<td>long</td>
</tr>
<tr>
<td>SCF_LogTime</td>
<td>long</td>
</tr>
<tr>
<td>SCF_RequestId</td>
<td>text</td>
</tr>
<tr>
<td>SCF_Duration</td>
<td>long</td>
</tr>
<tr>
<td>SCF_Alias</td>
<td>text</td>
</tr>
<tr>
<td>SCF_Qualifier</td>
<td>text</td>
</tr>
<tr>
<td>SCF_MemUsage</td>
<td>double</td>
</tr>
<tr>
<td>SCF_Level</td>
<td>text</td>
</tr>
<tr>
<td>SCF_Message</td>
<td>text</td>
</tr>
<tr>
<td>SCF_Type</td>
<td>text</td>
</tr>
<tr>
<td>SCF_StatusCode</td>
<td>long</td>
</tr>
</tbody></table>

For more information on other features such as real-time log search, delivery, and consumption, please see the [CLS documentation](https://intl.cloud.tencent.com/document/product/614). These features can be used in the [CLS Console](https://console.cloud.tencent.com/cls) directly.


### Sample real-time search
>?Before using the real-time search feature, please make sure that your SCF log service has been connected to the CLS platform and the index has been enabled for the log topic to be searched.
>
1. Log in to the CLS Console and select **[Log Search](https://console.cloud.tencent.com/cls/search)** on the left sidebar.
2. On the "Search and Analysis" page, select the desired log topic and time and enter the search syntax in the input box. This document uses `START` as an example.
The search syntax supports keyword search, fuzzy search, range search, and other search methods. For more information, please see [Legacy CLS Search Syntax](https://intl.cloud.tencent.com/document/product/614/37882).
3. Click **Search and Analysis** to view real-time log information.
