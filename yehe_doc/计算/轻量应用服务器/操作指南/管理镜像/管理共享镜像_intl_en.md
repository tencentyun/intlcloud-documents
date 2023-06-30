## Overview
Tencent Cloud allows you to share custom images between Lighthouse and CVM. You can customize image sharing as needed to implement offline migration between them. You can also use a shared image to quickly create instances and then get the needed components from them or add custom content to them.

<dx-alert infotype="explain" title="">
- Shared images do not take up the quota of custom Lighthouse instance images.
- A shared custom Lighthouse instance can be deleted only after sharing is canceled.
</dx-alert>

## Usage Limits
- Custom images can be shared only between Lighthouse and CVM instances in the same region under the same account.
- You cannot share the following custom images from CVM to Lighthouse:
 - Imported custom CVM instance images.
 - Custom images already shared from CVM to Lighthouse.
 - Custom images of entire CVM instances.
 - Custom images whose underlying operating system and version are not listed in [Supported Operating Systems](#supportOS).
 - Custom images without Cloud-init installed.

## Supported Operating Systems[](id:supportOS)

Images on the following underlying operating systems and versions can be shared:
- CentOS 6.8 or later
- Ubuntu 14.04 or later
- Debian 8.2 or later
- Windows Server 2012 or later
- TencentOS Server 2.4 or later

## Directions

### Sharing image to CVM[](id:shareToCVM)
1. Log in to the Lighthouse console and select <b>[Images](https://console.cloud.tencent.com/lighthouse/image)</b> on the left sidebar.
2. Select the region at the top of the **Image** page and click the **Custom image** tab.
3. On the right of the row of the target image, select **More** > **Share/Unshare**.
4. In the **Share Image** pop-up window, click **OK** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/1388a2a23765a99606352967e0fcd65c.png)
After sharing the image, you can view it on the [shared image](https://console.cloud.tencent.com/cvm/image/index) list page in the CVM console.


### Unsharing image to CVM
1. On the **Custom image** tab, select **More** > **Share/Unshare** on the right of the row of the target image.
2. In the **Unshare Image** pop-up window, click **OK** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/8205e83f5c743437b0e270f5300fcf70.png)


### Sharing image to Lighthouse[](id:shareToLH)

You can share a custom CVM instance image to Lighthouse in the following consoles:


<dx-tabs>
::: Lighthouse console
1. Log in to the Lighthouse console and select <b>[Images](https://console.cloud.tencent.com/lighthouse/image)</b> on the left sidebar.
2. Select the region at the top of the **Image** page and click the **Shared image** tab.
3. Click **Share CVM image**. In the **Share Image** pop-up window, select the target image as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/1f55e5bd04fb58f3bb092f9436a68c7d.png)
4. Click **OK**.
:::
::: CVM console
1. Log in to the CVM console and click <b>[Images](https://console.cloud.tencent.com/cvm/image/index)</b> on the left sidebar.
2. Select the region at the top of the **Image** page and click the **Custom image** tab.
3. On the right of the row of the target image, select **Share**.
4. In the **Share Image** pop-up window, select **Lighthouse** as the destination as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/30ca2641b57efe3be79125528e71f122.png)
5. Click **OK**.
:::
</dx-tabs>

### Unsharing image to Lighthouse

You can unshare a custom CVM instance image to Lighthouse in the following consoles:

<dx-tabs>
::: Lighthouse console
1. Log in to the Lighthouse console and select <b>[Images](https://console.cloud.tencent.com/lighthouse/image)</b> on the left sidebar.
2. Select the region at the top of the **Image** page and click the **Shared image** tab.
3. On the right of the row of the target image, click **Unshare** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7b1a9ef7aee1560f88b6213ff2e173ad.png)
4. In the **Unshare Image** pop-up window, click **OK**.

:::
::: CVM console
1. Log in to the CVM console and click <b>[Images](https://console.cloud.tencent.com/cvm/image/index)</b> on the left sidebar.
2. Select the region at the top of the **Image** page and click the **Custom image** tab.
3. On the right of the row of the target image, select **More** > **Unshare**.
4. On the **Shared image** tab on the image details page, select **Unshare** on the right of the row of the target image sharing record as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d89ff1c02727113f0380be255f09c185.png)
5. In the **Unshare** pop-up window, click **OK**.
:::
</dx-tabs>

## Related Operations

### Viewing image sharing status
You can view image information and sharing status on the custom image details page in the Lighthouse console:

1. Log in to the Lighthouse console and select <b>[Images](https://console.cloud.tencent.com/lighthouse/image)</b> on the left sidebar.
2. Select the region at the top of the **Image** page and click the **Custom image** tab.
3. Click the ID of the target image to enter its details page to view its information and sharing status.


### Using shared image to create instance
You can use an image shared to Lighthouse to create an instance quickly.

1. Log in to the Lighthouse console and select <b>[Images](https://console.cloud.tencent.com/lighthouse/image)</b> on the left sidebar.
2. Select the region at the top of the **Image** page and click the **Shared image** tab.
3. On the right of the row of the target image, click **Create instance** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/73562914d1ba988c7d8f92dd249a8e0e.png)
4. On the Lighthouse instance purchase page, select the configuration as need and create the instance.
Here, the shared instance is selected for **Image**, and you need to set other configuration items as instructed in [Purchase Methods](https://intl.cloud.tencent.com/document/product/1103/41404).

