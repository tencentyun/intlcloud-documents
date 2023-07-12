## Overview

The COS log analysis feature applies to various scenarios to help you efficiently extract key information from log files. This document describes how to add a COS log analysis function. After adding a function, see [Setting Log Analysis](https://intl.cloud.tencent.com/document/product/436/45570) to use this feature.

## Notes

- If you have added a COS log analysis rule to your bucket via the COS console, you can view the COS log analysis function you created in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **Do not** delete the COS log analysis function. Otherwise, your rule may not take effect.
- COS log analysis is supported in SCF-enabled regions, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see the [SCF documentation](https://www.tencentcloud.com/document/product/583).
- The log analysis feature depends on the SCF service, which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier according to [SCF pricing](https://intl.cloud.tencent.com/document/product/583/12281).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **App Integration** > **Extended Features** and find **COS Log Analysis**.
3. Click **Configure Analysis Feature** to enter the function rule configuration page.
4. Select a region to add the function and click **Add Function**. Configure the following information in the pop-up window:
 - **Function Name**: Uniquely identifies a function and cannot be modified after it is created. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: Select a COS bucket with the log analysis feature enabled.
 - **Execution Method**: Only async execution is supported. After the function is called, tasks will be executed asynchronously without returning the execution result. A longer running time is supported.
 - **Authentication Method**: Only SCF is supported.
 - **SCF Authorization**: SCF need to be authorized to read files from your bucket and save the result file to the specified folder.
5. Click **Confirm**.

   You can perform the following operations on the created function:
 - Click **Log** to view the historical running status.
 - Click **Details** to view detailed configuration rules.
 - Click **More** > **Edit** to modify a COS log analysis rule.
 - Click **More** > **Delete** to delete an unwanted COS log analysis rule.
