## Scenario

**Shared image** means that you share with **others users** a [**custom image**](https://intl.cloud.tencent.com/document/product/213/4942) you have created. Users can easily get shared images from each other to obtain necessary components and add custom contents.

> Tencent Cloud cannot guarantee the integrity or security of shared images. Please only use shared images from reliable sources.

## Notes
 - Each image can be shared with up to 50 users.
 - The name and description of shared images cannot be changed. They are used to create CVM instances only.
 - Images shared to other users do not occupy your own image quota.
 - Images shared to other users can be deleted, but you must cancel image sharing first. For more information, see [Cancel Image Sharing](/doc/product/213/7148). The obtained shared images can not be deleted.
 - Images can be shared to the same region with other accounts. To share the image to a different region, you need to copy it to the other region before sharing.
 - The shared images that you obtain from others cannot be shared to the third users.


## Directions

### Obtain the ID of the account with which you want to share the image

Tencent Cloud shared image is identified by the unique ID of the account with which you want to share the image. You can inform the other account to obtain his/her ID as follows:
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
2. Click the account name in the upper right corner and select **Account Information**.
3. View and record the account ID in the “Account Information” management page.
4. Send his/her account ID to you.

### Share images via console

 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[Images](https://console.cloud.tencent.com/cvm/image)**.
 3. Click the **Custom Image** tab to enter the custom image management page.
 4. Select the custom image you want to share in the custom image list and click **Share** on the right.
 5. In the pop-up “Shared Image** window, enter the ID of the account you want to share the image with, and click **Share**.
 6. Inform the other account to log in to the [CVM Console](https://console.cloud.tencent.com/cvm/), and select **Images**>**Shared Image** to view the image you have shared.
 7. To share the image with multiple users, repeat the steps above.

### Share images via API

You can use the ShareImage API to share images.
