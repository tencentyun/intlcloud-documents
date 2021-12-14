## Overview

**Shared image** means that you share with **others users** a [**custom image**](https://intl.cloud.tencent.com/document/product/213/4942) you have created. You can also obtain images shared by other users, get the necessary components, and add custom contents.

>! Tencent Cloud does not guarantee the integrity or security of shared images. Please only use shared images from reliable sources.
>

## Notes
 - Each image can be shared with a maximum of 50 Tencent Cloud users.
 - The name and description of shared images cannot be changed. They are used to create CVM instances only.
 - Images shared with other users do not occupy your own image quota.
 - A custom image that has been shared with others can be deleted, provided that you first cancel image sharing. For more information, see [Cancelling Image Sharing](https://intl.cloud.tencent.com/document/product/213/7148). The shared images that you obtain from others cannot be deleted.
 - Custom images can only be shared with accounts in the same region as the source account. To share an image with users in another region, you need to copy it to the target region before sharing.
 - The shared images that you obtain from others cannot be shared with the third users.

## Directions

### Obtaining the ID of the root account with which you want to share the image

Tencent Cloud shared image is identified by the unique ID of the root account with which you want to share the image. You can obtain the account ID of the other user as follows:
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. Click the account name in the top-right corner and select **Account Information**.
3. View and record the account ID.
4. Request the other user to send you the account ID.

### Sharing images via console

 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
 2. Click **[Images](https://console.cloud.tencent.com/cvm/image)** on the left sidebar.
 3. Click the **Custom Image** tab to enter the custom image management page.
 4. Select the custom image you want to share in the custom image list and click **Share** on the right.
 5. In the “Shared Image** pop-up window, enter the ID of the account you want to share the image with, and click **Share**.
 6.The other account needs to log in to the [CVM console](https://console.cloud.tencent.com/cvm/), and select **Images** > **Shared Image** to view the image you have shared.
 7. Repeat the steps above to share an image with multiple users.

### Sharing images via API

You can use the `ShareImage` API to share images. 
