## Overview

ECM provides public images, each of which contains the basic OS and initial components offered by Tencent Cloud for all users. If you want to quickly create multiple instances with the same configuration and applications, you can use the image creation feature to create a custom image and use it to create instances. ECM also allows you to import a custom image from the central cloud AZ to ECM instances. This document describes how to import and manage an image in the console.

## Prerequisites

You have created a custom image in the central cloud (i.e., CVM) AZ.

## Directions

### Importing image

1. Log in to the [ECM console](https://console.cloud.tencent.com/ecm/overview).
2. On the left sidebar, select **Image**.
3. On the image page, click **Import Image** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/5b3b0eb9d99d62e9eae271e0c9f43ebd.png)
4. In the pop-up window, select the region, OS, system architecture, and ID/name of the image to be imported and click **OK**.
>? ECM currently can retain up to 10 custom images.
>
After the import succeeds, the CVM data will be synced to ECM.

### Deleting image

1. Log in to the [ECM console](https://console.cloud.tencent.com/ecm/overview).
2. On the left sidebar, select **Image**.
3. On the image page, select the image to be deleted and click **Delete** in the **Operation** column .
>? Before performing this operation, check whether there is any ECM module using this image, and if so, it cannot be deleted.
>
4. In the pop-up window, click **OK**.




