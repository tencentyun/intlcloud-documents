## Overview

**Shared image** means that you share with **others users** a [**custom image**](https://intl.cloud.tencent.com/document/product/213/4942) you have created. You can also obtain images shared by other users, get the necessary components, and add custom contents.

<dx-alert infotype="notice" title="">
Tencent Cloud does not guarantee the integrity or security of shared images. Please only use shared images from reliable sources.
</dx-alert>


## Notes
 - Each image can be shared with a maximum of 50 Tencent Cloud accounts.
 - The name and description of shared images cannot be changed. They can only be used to create or reinstall CVM instances.
 - Images shared with other users do not occupy your own image quota.
 - A custom image that has been shared with others can be deleted, provided that you first cancel image sharing. For more information, see [Cancelling Image Sharing](/doc/product/213/7148). The shared images that you obtain from others cannot be deleted.
 - Custom images can only be shared with accounts in the same region as the source account. To share an image with users in another region, you need to copy it to the target region before sharing.
 - The shared images that you obtain from others cannot be re-shared.

## Directions

### Obtaining the ID of the root account to which you want to share the image

Tencent Cloud shared image is identified by the unique ID of the root account with which you want to share the image. You can obtain the account ID of the other user as follows:
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. Click the account name in the top-right corner and select **Account Information**.
3. View and record the account ID.
4. Request the other user to send you the account ID.

### Sharing images
<dx-tabs>
::: Sharing images via the console
 1. Log in to the CVM console and select [**Images**](https://console.cloud.tencent.com/cvm/image) on the left sidebar.
 3. Click the **Custom Image** tab to enter the custom image management page.
  3. In the custom image list, select the custom image you want to share and click **Share** in the **Operation** column.
 5. In the **Shared Image** pop-up window, enter the ID of the account with which you want to share the selected image, and click **Confirm**.
 6. Tell the other user to log in to the [CVM console](https://console.cloud.tencent.com/cvm/), and select **Images** > **Shared Image** to view the image you have shared.
Repeat the steps above to share an image with multiple users.
:::
::: Sharing images via an API
You can use the `ShareImage` API to share images.

:::
</dx-tabs>

## Related Operations

### Sharing image with Lighthouse
You can share a custom image between Lighthouse and CVM to implement fast offline service migration. You can also use a shared image to quickly create instances and then get the needed components from them or add custom content to them.



