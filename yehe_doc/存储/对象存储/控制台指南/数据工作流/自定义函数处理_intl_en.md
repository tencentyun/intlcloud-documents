## Overview

If the existing services or features of COS media processing cannot meet your needs, you can use the custom function processing feature of SCF to write core code logic in order to flexibly implement your business needs while reducing your development costs. For more information on SCF, see [Overview](https://intl.cloud.tencent.com/document/product/583/9199).

>?
> - Currently, the custom function processing feature can only be initiated in a [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
> - Using SCF for custom processing will incur fees, which will be charged by SCF. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).
> 

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the desired bucket.
4. On the left sidebar, click **Data Processing Workflow** > **Workflow** to enter the workflow management page.
5. Click **Create Workflow**.
6. Click **+** to the right of “Configure Workflow” to add a **custom function** node.
![](https://qcloudimg.tencent-cloud.cn/raw/5f198e30ed04fc8e8b093f3eeb09f106.png)

7. In the pop-up window, configure the following information.

 - Input Parameters: The input parameters specified with a custom function in a workflow don't need to be added manually. Instead, they can be obtained according to the node before the custom function.
 - Namespace: The created function is in the COS namespace by default.
 - Type: Select **Common feature** to quickly perform common operations on COS objects or **Custom** to configure other feature parameters.
 - Feature: The preset feature is supported when select the common feature.
 - Function: Currently, only functions that are executed asynchronously and have status tracking enabled are supported in a workflow.
 To create a function, click **Create Function** and configure the function as prompted.
8. After confirming that the configuration is correct, click **OK**.



