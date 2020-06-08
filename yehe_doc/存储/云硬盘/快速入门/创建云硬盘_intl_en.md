This document takes creating an empty cloud disk `cbs-test` in the Beijing region as an example to help you get started.

## Prerequisites
- Before creating a cloud disk, you need to [sign up for Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
- Make sure you have an available CVM in the region and availability zone (in this example, Beijing Zone 1) where the cloud disk is to be created. For information on CVM purchase and launch, see [Creating Instances](https://intl.cloud.tencent.com/document/product/213/4855).

## Directions
>In this example, an elastic premium cloud disk is purchased via the console. For more information on cloud disk creation, see [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744).

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Select **Beijing**, and click **Create**.
3. Configure the following parameters:
 - Availability Zone: select **Beijing Zone 1**.
 - Cloud Disk Type: select **Premium Cloud Storage**.
 - Capacity: 20 GB.
 - Disk Name: enter `cbs-test`.
 - Billing Mode: select **Pay-as-you-go**.
 - Period: select **1 month**.
4. Click **OK**.
5. After confirming the configurations, click **Confirm** and make the payment.
Return to the Cloud Block Storage list page. You can now view the purchased elastic cloud disk `cbs-test`, whose status is **To be mounted**.

## Subsequent Operations
After the cloud disk is created, you need to mount it on a CVM in the same availability zone to use it as a data disk. For information about this operation, see [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31645).
