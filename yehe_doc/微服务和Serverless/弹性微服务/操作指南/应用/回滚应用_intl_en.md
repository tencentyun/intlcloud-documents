## Overview

This document describes how to roll back a deployed application to its previous version.



## Prerequisites

You have [created and deployed an application](https://intl.cloud.tencent.com/document/product/1094/40362).



## Directions

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem) and click **Application Management** in the left sidebar to go to the application list page.
2. Select the target application and click the application ID to go to the application details page.
3. On the application details page, click **Rollback**.
   ![](https://main.qcloudimg.com/raw/190df67943d7b7f43b71ebbefe81713d.png)
4. In the pop-up rollback window, select a historical version to be rolled back to in the **Historical version** area.
   ![](https://main.qcloudimg.com/raw/9f127114ca8a410e1dbd67be791e8b50.png)
   - Up to 10 historical versions can be retained.
   - **Deployment Result**: **Deployed successfully** or **Failed to deploy**.
   - **Application Details**: displays the configuration information of the application deployment.
   - **Download**: If the historical version was uploaded using a JAR or WAR package, you can download the corresponding package in the list.
5. Click **Rollback** to redirect to the **Instance List** page. The system will roll back the application to the specified historical version in a rolling deployment mode.
