## Overview

SCF upgraded its log service on January 29, 2021 and was fully connected to Tencent Cloud CLS. The functions created before are gradually migrated by regions. For more information, please see [SCF Log Service Change Notification](https://intl.cloud.tencent.com/document/product/583/39328).

SCF provides the advanced search feature for functions created after January 29, 2021 and the migrated functions. The CLS search and analysis page is embedded in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). You can search for logs by using keyword or using query syntax to combine keyword.

<dx-alert infotype="explain" title="">
If your function was created before January 29, 2021 and has not been migrated, but you need to use more log analysis features, please see [Log Delivery Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/583/34876) to deliver function invocation logs to Cloud Log Service (CLS).
</dx-alert>



## Directions
You can use the advanced search feature in the following steps:
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. On the **Function Service** list page, select the name of the function for which to search for logs to enter the **Function Management** page.
3. On the **Function Management** page, select **Log Query** > **Advanced Retrieval**.
4. On the **Advanced Retrieval** page, you can search for logs by using keyword or using query syntax to combine keyword. **For more information on syntax rules, please see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439).**
5. After configuring the search criteria, you can click **Search and Analysis** on the right, and the results will be returned as shown below:
![](https://main.qcloudimg.com/raw/f0f51eecc4e0e034875a5834cb2c4862.png)



