## Overview

CLS allows you to use LogListener to collect CVM and Lighthouse logs. Before log collection, you need to install and deploy LogListener in CVM or Lighthouse. To quickly install and deploy LogListener in a number of CVM and Lighthouse instances, you can select CVM or Lighthouse instances in the console and batch distribute LogListener deployment tasks through an API to automatically complete LogListener installation and deployment (including `accesskey`, ID, and region configuration).

## Prerequisites

You have [installed TAT](https://intl.cloud.tencent.com/document/product/1147/46042) in CVM or Lighthouse.

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Machine Group Management** to enter the management page.
3. Click **Deploy Instances** in the top-right corner of the page.

4. On the **Deploy Instances** page, select the server type (CVM or Lighthouse). You can batch deploy LogListener for CVM and Lighthouse instances at the same time.

5. Select the target CVM or Lighthouse instances, enter the `SecretId` information (`SecretId` and `SecretKey`), and set **Machine label** in **Advanced Settings** as needed.

> ?
> - To install LogListener, you need to provide `SecretId` and `SecretKey` for uploading logs. They can be obtained as instructed in [Viewing Acquisition Method](https://console.cloud.tencent.com/cam/capi).
> - Make sure that the account of the entered key information has the permission to upload logs. For detailed directions on how to configure permissions, see [CAM Access Management](https://www.tencentcloud.com/document/product/614/32854).
> - If your machine IP changes frequently, we recommend that you configure the machine label as instructed in [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).



6. Click **Next**.
7. On the instance installation page, click **Next** when the installation **Status** changes to **Completed**, which indicates that the installation is completed.
>? If the installation fails, move the cursor over to the **Status** of the instance installation to view the failure causes.



8. On the machine group importing page, select an existing machine group or create a machine group as required, and click **Import**.


>? The version of the LogListener deployed via batch deployment is 2.6.0 or later.
