## Scenario
This document describes how to cancel custom image sharing. You can cancel your image sharing status with other users at any time. This does not affect instances created by other users using this shared image, but they can no longer see the image nor create new instances using this image.

## Directions
<dx-tabs>
::: Cancel image sharing through the console
 1. Log in to the CVM Console.On the left sidebar, click [Images](https://console.cloud.tencent.com/cvm/image/index?rid=1).
 2. Select **Custom Image** tab to enter the custom image management page.
 3. In the custom image list, select the custom images you want to cancel sharing and click **More** > **Cancel Sharing**.
![](https://qcloudimg.tencent-cloud.cn/raw/2babd57218139864c0cff8b65db5bd3c.png)
 4. On the new page, select the unique ID of the account from which you want to cancel the image sharing and click **Cancel Sharing**.
 5. In the pop-up window, click **OK** to cancel image sharing.
:::
:::  Cancel image sharing through API
You can use the ModifyImageSharePermission API to cancel image sharing. For more information, see [ModifyImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33268).
:::
</dx-tabs>
