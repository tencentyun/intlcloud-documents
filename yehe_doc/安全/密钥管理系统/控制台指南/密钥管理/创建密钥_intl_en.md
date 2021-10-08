## Scenarios
A CMK can be created in the KMS console or by calling the CreateKey API. After creation, you can manage the CMK by enabling, disabling, rotation and granting permission. This document describes how to create a CMK in the console.


## Directions

1. Log in to the [KMS Console](https://console.cloud.tencent.com/kms2).
2. Select the region for which you want to create a key and click **Create**.
![](https://main.qcloudimg.com/raw/717599b42949a9ba17dd858f2d7feac1.png)
3. Enter the following information in the pop-up box:
 - Key Name: This is required and must be unique within the region. It can contain letters, numbers, `_`, `-`, and cannot begin with "KMS-".
 - Description: This is optional and used to specify the type of data to be protected, or the application to be used in conjunction with the CMK.
 - Tag: This is optional. [Tag](https://intl.cloud.tencent.com/document/product/651/13334) is a Tencent Cloud resource management tool that allows you to categorize, search and aggregate keys.
 - Key Usage: This is required and supports symmetric encryption and decryption, asymmetric encryption and decryption, or asymmetric signature verification.
  - Key Material Source: This is required. You can choose to generate the key in KMS or import your own key.
![](https://main.qcloudimg.com/raw/2e2ef4eff0aa8fd823b9f3c86da26779.png)
4. Click **OK** to go back to the key list, and then you can see the new key at the top of the list.




