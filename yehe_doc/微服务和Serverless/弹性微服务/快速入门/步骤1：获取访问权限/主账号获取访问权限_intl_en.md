## Overview

As TEM needs to access APIs of other Tencent Cloud products, you need to create service roles and grant TEM those roles.

## Preparation

You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

>?After you register a Tencent Cloud account, the system will create a root account for you by default, which is used to quickly access Tencent Cloud resources.

## Directions

If you use TEM for the first time, you need to create the `TEM_QCSLinkedRoleInAccessCluster` and `TEM_QCSLinkedRoleInTEMLog` service roles as follows to grant you the permissions to access resources of other Tencent Cloud products.

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem) with the **root account**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/9d3dc63147c10a39be367806c0871d3f.png)
2. Click **Authorize Now** to enter the [CAM console](https://console.cloud.tencent.com/cam/overview), click **Grant**, and the `TEM_QCSLinkedRoleInAccessCluster` service role will be created to grant you the permissions to access resources of Tencent Cloud products other than CLS.
   ![](https://qcloudimg.tencent-cloud.cn/raw/bfc5e42cacfd469b62aa4e7199ff163a.png)
3. Return to the [TEM console](https://console.cloud.tencent.com/tem) and click **Authorized**.
4. On the left sidebar, click **Application management**. In the pop-up window, click **Authorize Now** to enter the [CAM console](https://console.cloud.tencent.com/cam/overview), click **Grant**, and the `TEM_QCSLinkedRoleInTEMLog` service role will be created to grant you the permission to access CLS resources.



   
