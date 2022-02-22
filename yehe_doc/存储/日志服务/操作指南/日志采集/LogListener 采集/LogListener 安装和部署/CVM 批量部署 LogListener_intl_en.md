## Overview

CLS supports log collection via LogListener for Tencent Cloud Virtual Machines (CVMs). Before log collection, you need to deploy LogListener on CVM instances. If you need to deploy LogListener on a large number of CVM instances, you can perform batch deployment in the CLS console. Batch deployment will deploy configurations including AccessKeys, IDs, and regions.

## Prerequisites

TencentCloud Automation Tools (TAT) is installed on the target CVM instances.

## Directions
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Overview** to go to the overview page.
3. Choose **Fast Integration** > **Cloud Product Logs**, and click **CVM**.

4. On the batch deployment configuration page, select the target CVM instances, enter `SecretId` information (`SecretId` and `SecretKey`), and set advanced configuration items accordingly.

5. Click **Next**.
6. On the instance installation page, click **Next** when the installation **Status** changes to **Completed**, which indicates that the installation is completed.
>? If the installation fails, move the cursor over to the **Status** of the instance installation to view the failure causes.
> 

7. On the machine group importing page, select an existing machine group or create a machine group as required, and click **Import**.

>? The version of the LogListener deployed via batch deployment is 2.6.0 or later.
>



