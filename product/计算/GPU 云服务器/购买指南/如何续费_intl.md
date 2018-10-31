You can renew or set auto renewal for a prepaid instance at any time before the end of its lifecycle to prevent data loss and service interruption due to termination of instance upon its expiration.
## Manual Renewal
### Manual renewal on the console
Renew instances manually on the console by following the procedure below:
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
2. Select **GPU G2** and the instance you want to renew, and then click **Renew** in the operation column on the right. </br>
![](//mc.qcloudimg.com/static/img/3323b4ba0adfe4730812145e8ed6a952/image.png)
3. In the pop-up box of CVM renewal, select the renewal period and whether to adjust the bandwidth, and then click **OK**.
![](//mc.qcloudimg.com/static/img/680969b368d7fd33e18f703938a4b6ff/image.png)
4. After making the payment, the GCC instance is renewed.

### Renewal via API
You can use the API RenewInstance to renew instances. For more information, see [Instance Renewal (Prepaid) API>>](/doc/api/229/1348).
## Auto Renewal
### Setting Auto Renewal via Console
You can set auto renewal for prepaid GCC instances to eliminate the need to renew the instances whenever they are about to expire:
1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com), move the mouse cursor to the fees at the top right corner, and then select **Renew** in the menu.
![](//mc.qcloudimg.com/static/img/6b96b320741ddc2ba3a5a3264bafa923/image.png)
2. For the GCC instances you want to renew, click **Set Auto Renewal** on the operation column on the right.
![](//mc.qcloudimg.com/static/img/8786cdaf0d52401b8b192afdfe1ca624/image.png)
3. Click **OK** in the pop-up box of auto renewal.

For instances set to auto renewal, the charge for the next billing period is automatically deducted from the balance on the expiry date. If you have a sufficient account balance, the instance goes into the next billing period automatically.
> **Note:**
Batch renewal is not supported for GCC instances.

### Setting Auto Renewal via API
You can use the API SetAutoRenew to set auto renewal for instances. For more information, see [Set Auto Renewal for Instances via API>>](/doc/api/229/1746).
## Renewal to the Same Expiry Date
Tencent Cloud allows you to renew instances to the same expiry date. By specifying the same expiry date for cloud products created at different times, you can be freed from repetitive renewal operations for services with different expiry dates and stop all services at the specified expiry date to save costs. For more information about renewal for same expiry date, see [Set Same Expiry Date>>](/doc/product/285/1894#.E8.AE.BE.E7.BD.AE.E7.BB.9F.E4.B8.80.E5.88.B0.E6.9C.9F.E6.97.A5)..

