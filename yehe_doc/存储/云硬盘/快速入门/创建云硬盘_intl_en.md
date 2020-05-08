This document will teach you how to quickly create a CBS cloud disk by creating an empty cloud disk called `cbs-test` in the Beijing region as an example.

## Prerequisites
- Before you create a cloud disk, you need to [sign up for Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985), and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
- Make sure that you have an available CVM in the region and availability zone (in this example, Beijing Zone 1) where the cloud disk is to be created. For information on how to buy and start a CVM, see [Creating Instances](/doc/product/213/4855).

## Directions
>In this example, an elastic Premium cloud disk is purchased via the console. For more information on creating cloud disks, see [Creating Cloud Disks](/doc/product/362/5744).

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Select **Beijing**, and click **Create**.
3. Configure the following parameters:
 - Availability Zone: select **Beijing Zone 1**.
 - Cloud Disk Type: select **Premium Cloud Storage**.
 - Capacity: set 20 GB.
 - Disk Name: enter `cbs-test`.
 - Billing Mode: select **Pay-as-you-go**.
 - Period: select **1 month**.
4. Click **OK**.
5. After you confirm the specifications, click **Confirm** to make the payment.
Return to the Cloud Block Storage list page, now you can find the purchased elastic cloud disk `cbs-test`, whose status is displayed as **To be mounted**.

## See Also
After the cloud disk is created, you need to first mount it on a CVM in the same availability zone to use it as a data disk. For more information about this operation, see [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31645).
