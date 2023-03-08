Before reading this document, make sure you understand the [basic concepts](https://www.tencentcloud.com/document/product/1167/51910) of CVD first.

## Prerequisites

Before creating a CVD instance, you must complete the following operations:
1. Sign up for a [Tencent Cloud account](https://www.tencentcloud.com/en/account/register).
2. Activate [CVD](https://console.cloud.tencent.com/cvd).
## Directions

1. Log in to the [CVD purchase page](https://buy.cloud.tencent.com/cvd) and choose the specifications:

| Item                    | Description                                                         |
| --------------- | ------------------------------------------------------------ |
| Billing mode | **Monthly subscription** or **Pay-as-you-go** |
| Region | For better access experience, we recommend you choose the region closest to your business location. |
| Desktop type | Currently, only personal desktops (each end user is assigned separate desktop resources) are available. |
| Network | Select a VPC and subnet. If you don't have a VPC or existing VPCs don't meet your needs, you can create one. If your CVD instance requires internet access, configure it in NAT gateway of the VPC console. |
| Compute resources | CVD offers different combinations of CPU and memory specifications. Choose the one that fits your needs. |
| Management unit        | Management units come in two types – standard and graphic. When you buy a desktop instance, the system will automatically select a management unit according to the compute resources you purchase. |
| Image | CVD provides public images and Tencent Cloud office images. The latter come with preinstalled office applications such as WeCom, Tencent Meeting, and Tencent Docs. |
| Storage resources - system disk | Select an SSD or premium system disk for the instance and specify the disk size. A system disk stores OS resources. Note that the system disk of the instance must be larger than that of the image used. |
| Storage resource - data disk | (Optional) Select an SSD or premium data disk for the instance and specify the disk size. A data disk stores user data. |
| Quantity | The number of CVD instances to purchase. |
| Purchase period        | The number of months to purchase.                                     |
| Desktop name | The desktop name. If you leave this field empty, a unique name in the format of "instance name + month and day of creation + three-digit random number + image ID" will be used. |
| Auto-renewal | In the monthly subscription billing mode, you can select **When a package expires, it will be automatically renewed for one month if your account has sufficient balance.** After the instance is created, you can modify its auto-renewal settings in the console. For details, see [Renewing CVD Instance](https://www.tencentcloud.com/document/product/1167/51928#automatically). |

2. After completing the above configuration, confirm that everything is correct and click **Buy Now**.

3. On the order confirmation page, check the details of your order and make the payment.

4. After making the payment, click **Go to the console** to manage your CVD instances.
