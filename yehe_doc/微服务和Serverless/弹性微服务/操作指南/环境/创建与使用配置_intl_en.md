## Overview

This document describes how to create and use configurations in the TEM console.



## Directions

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem).
2. On the **Environment** page, select a deployment region and click **View Details** under the target environment block to go to the environment details page.
3. Select the **Configuration Management** tab at the top of the page, click **Create**, and enter configuration details.
   ![](https://main.qcloudimg.com/raw/0d21038c62529740595082de292ba811.png)
   
   - **Name**: enter the name of the configuration file.
   - **Content:** enter the configured key-value pairs.
4. Click **Submit** to complete the creation.

   

## Related Operations

- **Modifying a configuration item:** click **Edit** in the **Operation** column of the target configuration item and modify the configuration in the pop-up window.
- **Deleting a configuration item:** click **Delete** in the **Operation** column of the target configuration item and click **OK** in the pop-up window.
>?Before deleting a configuration that is associated with an application, you need to disassociate it from the application first.

- **Associating a configuration with an application:** go to the **Deploy Application** page, set the path to the container to which the configuration item is mounted in the **Configuration Setting** area. For operation details, please see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
  ![](https://main.qcloudimg.com/raw/c952bcdc439356c0244e8f2bbff0ed15.png)
