## Overview
While purchasing CVMs on the CVM purchase page, you can generate the OpenAPI best practice reusable scripts with the selected configurations. You can then use these codes to purchase CVM instances with the same configurations.

## Prerequisites
- You have logged in to the Tencent Cloud console and accessed the CVM [**Custom Configuration**](https://buy.cloud.tencent.com/cvm?tab=custom) page.
- You have completed CVM configurations and entered the **Confirm Configuration** page. To learn about how to configure parameters, see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).

## Directions
1. On the **Confirm Configuration** page, click **Generate API Explorer Reusable Scripts** as shown below:
![](https://main.qcloudimg.com/raw/7c095b6809c8815b15d4fe2c45b89305.png)
2. You can view the following information in the pop-up window.
![](https://main.qcloudimg.com/raw/5fba656be4ee0977245a7778f6a4c910.png)
 - **API Workflow**: provides the description and actual parameters of the `RunInstances` API based on the selected configurations. The parameters marked with “*” are required for the API. You can hover over the data to display it completely.
 - **API Script**: generates codes in Java and Python programing languages. Select the Java or Python tab as needed, click **Copy Script** in the top-right corner, and save the codes to purchase CVM instances that contain the same configurations.
>?
>- The instance password will not be displayed on the page or script codes for security reasons. Please modify it by yourself. 
>- The collective expiry date cannot be set in the API Explorer reusable script. You need to set it after creating the CVM.
