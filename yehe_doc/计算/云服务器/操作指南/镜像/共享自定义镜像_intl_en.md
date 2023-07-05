## Overview

A **shared image** is a [**custom image**](https://intl.cloud.tencent.com/document/product/213/4942) that a user shared to other users. With a shared image, you can get the necessary components from other users and add your custom contents.

<dx-alert infotype="notice" title="">
Tencent Cloud does not guarantee the integrity or security of shared images. Please only use shared images from trusted sources.
</dx-alert>


## Limits
 - Each image can be shared with a maximum of 50 Tencent Cloud accounts.
 - You can not change the name and description of the images shared from others. They can only be used to create or reinstall CVM instances.
 - When you share an image to others, the shared replicas do not count against your image quota.
 - If you need to delete a custom image that is shared with others, you need to cancel all the sharing relations first. For more information, see [Cancelling Image Sharing](/doc/product/213/7148). You can not delete an image shared from others.
 - Custom images can only be shared with accounts in the same region as the source account. To share an image with users in another region, you need to copy it to the target region before sharing.
 - The shared images that you obtain from others cannot be re-shared.

## Directions

### Obtaining the ID of the root account to which you want to share the image

To share an image to another user, you need to know their root account ID. They can check their root account ID as instructed below:
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. Click the account name in the top-right corner and select **Account Information**.
3. View and note down the account ID.
4. Notify the other party to send the obtained account ID to itself.

### Sharing images
<dx-tabs>
::: Sharing images in the console
 1. Log in to the CVM console and select [**Images**](https://console.cloud.tencent.com/cvm/image) on the left sidebar.
 2. Click the **Custom Image** tab to enter the custom image management page.
  3. In the custom image list, select the custom image you want to share and click **Share** in the **Operation** column.
 4. In the **Shared Image** pop-up window, enter the ID of the account with which you want to share the selected image, and click **Share**.
 5. Tell the other user to log in to the [CVM console](https://console.cloud.tencent.com/cvm/), and select **Images** > **Shared Image** to view the image you have shared.
Repeat the steps above to share an image with multiple users.
:::
::: Sharing images via an API
You can use the `ShareImage` API to share images.

:::
</dx-tabs>

## Related Operations

### Sharing image with Lighthouse
You can share a custom image between Lighthouse and CVM to implement fast offline service migration. You can also use a shared image to quickly create instances and then get the needed components from them or add custom content to them.



