## Overview
You can create a custom image in addition to using Lighthouse application images and system images. The custom image can be used to quickly create Lighthouse instances with the same configurations as the image in the Lighthouse console.

## Notes
- Up to 20 custom images can be created in each region.
- A free tire of five custom images is provided in each region, and excessive images will incur fees. For more information, see [ Billing Overview](https://intl.cloud.tencent.com/document/product/1103/41403).
- If your account has overdue payments:
 - The custom image feature will be disabled, and you cannot create more custom images.
 - All custom images (including those within the free tier) under your account will be isolated in the **to be repossessed** status and become unavailable. If you don't top up your account within seven days, the custom images will be automatically released.
- The creation process takes ten minutes or more, which depends on the data size of the instance. Prepare in advance to avoid business impacts.
- Currently, cross-region replication of custom images is not supported. You can regularly check out the [TencentCloud Lighthouse](https://intl.cloud.tencent.com/products/lighthouse) page to get the latest information.

## Directions
### Creating custom image[](id:createCustom)
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index)。
2. On the instance list page, select the instance for which to create a custom image to enter the instance details page.
3. In "Application Information" on the instance details page, select Create image as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/b8664efd7d6a8ecee04eaebc90e4e07b.png)
4. In the "Enter image information" step in the "Create custom image" pop-up window, enter the image name and image description, and click Next: Shut down the instance as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/5b51a5b38db83faaba4771c2d513268e.png)
5. In the "Shutdown instance" step, select "Agree to a forced shutdown" and click Create image.
After the custom image is created, you can go to the [custom image](https://console.cloud.tencent.com/lighthouse/image) list page to view it.

### Deleting custom image
1. Log in to the Lighthouse console and select **[Custom Image](https://console.cloud.tencent.com/lighthouse/image)**on the left sidebar.
2. At the top of the **Custom Image** page, select the region where the target image is located.
3. Select**More** > ** Delete**on the right of the target image in the list.
4. In the "Delete image" pop-up window, click**OK**to delete the image.

## Relevant Operations
### Using custom image to create instance
You can use a custom image to quickly create a Lightweight instance in the following steps:
1. Log in to the Lighthouse console and select **[Custom Image](https://console.cloud.tencent.com/lighthouse/image)**on the left sidebar.
2. At the top of the **Custom Image** page, select the region where the target image is located.
3. Select Create instance on the right of the target image in the list to enter the Lighthouse instance purchase page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/b7349a5215486b7b16fe9e31c2727064.png)
4. On the Lightweight instance purchase page, select other configuration items of the instance as instructed in [Purchase Methods](https://intl.cloud.tencent.com/document/product/1103/41404) .
<dx-alert infotype="explain" title="">
As custom images don't have a unified template and are created based on your own data, the instances created by using them don't have the**Pre-installed Application**tab.
</dx-alert>

### Viewing the information of custom images in the current region
You can view the information of existing custom images in a specific region in the following steps:
1. Log in to the Lighthouse console and select **[Custom Image](https://console.cloud.tencent.com/lighthouse/image)**on the left sidebar.
2. At the top of the **Custom Image** page, select the region where the target image is located.
3. Then, you can view the total number of custom images, free tier, and estimated price information in the current region on the page as shown below:
<dx-alert infotype="explain" title="">
- A free tire of five custom images is provided in each region.
- Once your account has overdue payments, all custom images (including those within the free tier) under your account will be isolated in the **to be repossessed** status and become unavailable. If you don't top up your account within seven days, the custom images will be automatically released.
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/3bbc42da52aae39ec755070dfaf1dfdf.png"/>


## Documentation
- [Overview](https://intl.cloud.tencent.com/document/product/1103/41261)
- [Billing Overview](https://intl.cloud.tencent.com/zh/document/product/1103/41403?lang=zh&pg=#.3Ca-id.3D.22customizeos.22.3E.E8.87.AA.E5.AE.9A.E4.B9.89.E9.95.9C.E5.83.8F.E8.AE.A1.E8.B4.B9.E6.A6.82.E8.BF.B0.3C.2Fa.3E)
