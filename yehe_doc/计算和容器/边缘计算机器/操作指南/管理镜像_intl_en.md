## Overview

ECM provides public images, each of which contains the basic OS and initial components offered by Tencent Cloud for all users. If you want to quickly create multiple instances with the same configuration and applications, you can use the image creation feature to create a custom image and use it to create instances. ECM also allows you to import a custom image from the central cloud AZ to ECM instances. This document describes how to import and manage an image in the console.

## Prerequisites

You have created a custom image in the central cloud (i.e., CVM) AZ.

## Directions

### Importing image

1. Log in to the [ECM console](https://console.cloud.tencent.com/ecm/overview).
2. On the left sidebar, select **Image**.
3. On the image page, click **Import Image** as shown below:
![](https://main.qcloudimg.com/raw/9adc9f0bb026de64c9c61291d66ea21c.png)
4. In the pop-up window, select the region, OS, system architecture, and ID/name of the image to be imported and click **OK**.
>? ECM currently can retain up to 10 custom images.
>
![](https://main.qcloudimg.com/raw/11c9a151236a7fc705c1a29ddd7f7ee3.png)
After the import succeeds, the CVM data will be synced to ECM.

### Deleting image

1. Log in to the [ECM console](https://console.cloud.tencent.com/ecm/overview).
2. On the left sidebar, select **Image**.
3. On the image page, select the image to be deleted and click **Delete** in the **Operation** column as shown below:
>? Before performing this operation, check whether there is any ECM module using this image, and if so, it cannot be deleted.
>
![](https://main.qcloudimg.com/raw/f6a897e9acb12f015777a1612360aca3.png)
4. In the pop-up window, click **OK**.




