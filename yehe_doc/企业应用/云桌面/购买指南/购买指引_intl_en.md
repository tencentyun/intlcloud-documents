Before reading this document, make sure you understand the [basic concepts](https://www.tencentcloud.com/document/product/1167/51910) of CVD first.

## Prerequisites

Before creating a CVD instance, you must complete the following operations:
1. Sign up for a [Tencent Cloud account](https://www.tencentcloud.com/en/account/register) and complete [enterprise identity verification](https://www.tencentcloud.com/document/product/378/10496).
2. Activate the [CVD service](https://console.cloud.tencent.com/cvd).
>?Currently, the CVD service is available only to enterprise users. You can activate it after completing the enterprise identity verification.

## Directions
Log in to the [CVD purchase page](https://buy.cloud.tencent.com/cvd) and configure the following items as prompted:

| Configuration Item | Description |
| ----------------- | --------------- |
| Billing mode | Select **Monthly subscription** or **Pay-as-you-go** as appropriate. |
| Region | Select a region. We recommend you choose the region closest to your actual business, which can improve the access experience. |
| Desktop type | Currently, the personal desktop type is available; that is, each user is assigned separate desktop resources. |
| Network | Select a VPC/subnet. If you don't have a VPC or existing VPCs don't meet your needs, you can create a new one as needed. If your CVD instance requires internet access, configure the NAT gateway in the console. |
| Compute resources | The compute resources of a CVD instance include different combinations of CPU and memory specifications, which you can select flexibly based on your business needs. |
| Image | CVD provides public images and Tencent Cloud office images, which you can select flexibly based on your business needs. The latter comes with preinstalled office applications such as WeCom, Tencent Meeting, and Tencent Docs. |
| Storage resource - system disk | Select an SSD or premium cloud disk of the desired size as the system disk of the CVD instance to sustain OS resources. The system disk must be larger than the size of the image used when an instance is launched. |
| Storage resource - data disk | (Optional) Select an SSD or premium cloud disk of the desired size as the data disk of the CVD instance to sustain user data resources. |
| Quantity | Specify the number of CVD instances of this specification to be batch purchased. |
| Purchase period | Specify the usage period of the CVD instance. |
| Desktop name | Customize the instance name. If you leave this field empty, the unique instance name in the format of instance model + month and day + three-digit random number + image ID will be used by default. |
| Auto-renewal | In the monthly subscription billing mode, you can select **When a package expires, it will be automatically renewed for one month if your account has sufficient balance.** to enable the auto-renewal feature. After successfully creating the instance, you can modify the current auto-renewal settings as instructed in [Auto-Renewal](https://www.tencentcloud.com/document/product/1167/51928). |


1. After completing the above configuration, confirm that everything is correct and click **Buy now**.
2. On the **Check the order** page, check the details and pay for the order.
3. After making the payment, click **Go to the console** to manage your CVD instance.
