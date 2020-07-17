## Overview

When Serverless Cloud Function (SCF) is used for function computing, a high number of function execution logs are generated. As connected to Tencent Cloud CLS, SCF can collect function execution logs and push them to CLS in real time. CLS supports multiple log operations, such as search, shipping, and consumption.
![](https://main.qcloudimg.com/raw/77c64b4a7673bb73e4531243ba3e2523.png)

## Directions

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and create a logset and a log topic. Set the region of the logset to the same as that of the SCF. Currently, cross-region log pushing is not supported. For more information, see [Creating a logset and a log topic](https://intl.cloud.tencent.com/document/product/614/31592).
2. To search for logs, you need to enable index manually. If you have done so, skip Steps 2-5.
   Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and click **Logset**. Select the logset you want, and click *Manage** under the **Operation** column to enter the logset details page.
	 ![](https://main.qcloudimg.com/raw/363e1286f9b00ec6822964368680cbfe.png)
3. Select the **Index Configuration** tab.
4. Click **Edit**, toggle on **Index Status**, **Full-Text Index** and **Key-Value Index**, and then add key-value indexes.
	 ![](https://main.qcloudimg.com/raw/b74e2909c6b147961aed8ab9ba4381bc.png)
5. Once completed, click **Save**.	 
   
   >For more operations, such as real-time log search, log shipping and consumption, log in to the [CLS Console](https://console.cloud.tencent.com/cls). For more features, see [CLS Overview](https://intl.cloud.tencent.com/document/product/614).
  #### SCF log fields
<table>
<thead>
<tr>
<th>Field</th>
<th>Meaning</th>
<th>Type</th>
</tr>
</thead>
<tbody><tr>
<td>SCF_RequestId</td>
<td>Request ID</td>
<td>text</td>
</tr>
<tr>
<td>SCF_Namespace</td>
<td>Namespace</td>
<td>text</td>
</tr>
<tr>
<td>SCF_FunctionName</td>
<td>Function name</td>
<td>text</td>
</tr>
<tr>
<td>SCF_Qualifier</td>
<td>Version</td>
<td>text</td>
</tr>
<tr>
<td>SCF_StartTime</td>
<td>Start time</td>
<td>long</td>
</tr>
<tr>
<td>SCF_Message</td>
<td>Log content</td>
<td>text</td>
</tr>
<tr>
<td>SCF_Level</td>
<td>Log level</td>
<td>text</td>
</tr>
<tr>
<td>SCF_Index</td>
<td>Log line No.</td>
<td>long</td>
</tr>
<tr>
<td>SCF_Alias</td>
<td>Function alias</td>
<td>text</td>
</tr>
</tbody></table>
6. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/index?rid=1). Click **Function Service** in the left sidebar to enter the functions list page.
7. Click the name of the function for real-time log collection, after which the **Function Configuration** page is displayed. In the upper-right corner, click **Edit** to edit the function information.
8. Configure the logset and log topic created in Step 1 for the function service, then click **Save**.

## Log Search Examples

Before using the real-time search feature, make sure that your SCF logs are connected to CLS and that index is enabled for the log topic to be searched. If index is not enabled, see [Enabling Index](https://intl.cloud.tencent.com/document/product/614/16981).

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and click **Log Search** in the left sidebar to enter the log search page.
2. Select the time range and log topic before using the search box. The search syntax supports searching by keyword, fuzzy match, and scope. For more information, see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439).
3. Now, click **Search Analysis** to begin searching for logs.
   Example 1: `SCF_StartTime:1583233118007` searches for logs with a timestamp 1583233118007.
   ![](https://main.qcloudimg.com/raw/157c2f861065cbad78973fc4e0258f2b.png)
   Example 2: `SCF_Index:2` searches for logs matching an index of 2.
   ![](https://main.qcloudimg.com/raw/852ffa027fe4427d10f98e9c73902d26.png)

