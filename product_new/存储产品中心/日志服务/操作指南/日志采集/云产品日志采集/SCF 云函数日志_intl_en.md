## Overview
When Serverless Cloud Function (SCF) is used for function computing, a high number of function execution logs are generated. SCF is connected to CLS of Tencent Cloud, and SCF can collect function execution logs and push them to CLS in real time. CLS supports multiple log operations, such as search, shipping, and consumption.
![](https://main.qcloudimg.com/raw/77c64b4a7673bb73e4531243ba3e2523.png)

## Prerequisites

[CLS](https://intl.cloud.tencent.com/product/cls) is activated.



## Access directions

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and create a logset and a log topic. Set the region of the logset to the same as that of the SCF. Currently, cross-region log pushing is not supported. For more information, see [Creating a Logset and a Log Topic](https://intl.cloud.tencent.com/document/product/614/31592).
2. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/index?rid=1). Click **Functions** In the left sidebar to enter the function service list page.
3. Click the name of the function for which logs need to be collected in real time, after which the **Function Configuration** page is displayed. In the upper-right corner of the page, click **Edit** to edit the function information.
4. On the **Function Configuration** page, configure the logset and log topic created in Step 1 for the function service, then click **Save**.
   ![](https://main.qcloudimg.com/raw/363e1286f9b00ec6822964368680cbfe.png)
5. Now you have accessed the CLS platform. To search logs, manually enable the index.
   Log in to the [CLS Console](https://console.cloud.tencent.com/cls), click **Logset Management**, and choose the target logset and log topic. On the log topic tab, in the **Operation** column on the right, choose **Configure** > **Index Configuration** to enter the index configuration page.
   ![](https://main.qcloudimg.com/raw/4a21ab6302808048c8a59b0aa20e1f71.png)
6. In the upper-right corner, click **Edit**, enable **Index Status** and **Full-Text Index**, then click **Save**.
   ![](https://main.qcloudimg.com/raw/b74e2909c6b147961aed8ab9ba4381bc.png)
   > For more operations, such as real-time log search, log shipping and consumption, log in to the [CLS Console](https://console.cloud.tencent.com/cls). For more features, see the [CLS Overview](https://intl.cloud.tencent.com/document/product/614) document.

## Real-time search example

Before using the real-time search feature, make sure that your function service logs can access the CLS platform and that the index feature is enabled for the log topic to search. If index is not enabled, see the [Enabling Index](https://intl.cloud.tencent.com/document/product/614/16981) document.

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls). Click **Log Search** in the left sidebar to enter the log search page.
2. Select the time range and log topic to search, then enter the search syntax in the input box. The syntax supports search by keyword, fuzzy match, and scope. For more information, see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/16982).
3. Click **Search** to search the logs.
   The following figure shows how to search for logs containing Memory.
   ![](https://main.qcloudimg.com/raw/42630d28d44bc8fdc69f53b94ef0a087.png)
