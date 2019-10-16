This article will teach you how to quickly create a cloud disk by creating an empty cloud disk called `cbs-test` in the Beijing region as an example.

## Prerequisites
- Before you create a cloud disk, you need to [sign up for Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985), and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
You must ensure that you have an available CVM under the region and availability zone where you create the cloud disk (in this example, Beijing Zone 1). For information on how to purchase and launch a CVM, see [Purchase and launch a CVM](https://intl.cloud.tencent.com/document/product/213/4855).

## Directions
>In this example, you can purchase an elastic HDD cloud disk through the console. For more information on how to create a cloud disk, see [Creating a cloud disk](https://intl.cloud.tencent.com/document/product/362/5744).

1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs).
2. Select **Beijing**, click **New**.
3. Configure the following parameters.
 - Availability Zone: Select **Beijing Zone 1**.
 - Cloud Disk Type: Select **HDD cloud disk**.
 - Capacity: Set 20GB.
 - Disk Name: Enter `cbs-test`.
 - Billing Mode: Select **Pay as you go**.
 - Period: Select **1 month**.
4. Click **OK**.
5. After you confirm the specifications, click **Confirm Purchase**, to make the payment.
Return to the cloud disk list page. You can see the purchased cloud disk. The elastic cloud disk that you just purchased is not named by default, and is displayed as **to be mounted**.

## Subsequent Operations
After the cloud disk is created, you need to first mount it on a CVM in the same availability zone to use it as a data disk. For more information about this operation, see [Mounting a cloud disk](https://intl.cloud.tencent.com/document/product/362/31594).

