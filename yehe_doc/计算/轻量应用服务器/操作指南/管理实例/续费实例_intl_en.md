## Overview
This document describes how to renew a Lighthouse instance manually or set auto-renewal for it.



## Directions
### Manual renewal

You can renew an instance or batch renew multiple instances manually in the following steps based on the instance status:
<dx-tabs>
::: Renewing running instances[](id:running)

#### Renewing one instance

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. On the **Instances** page, enter the details page of the target instance.
3. Select **Renew** in the **Billing information** section. In the **Renew instance** pop-up window, select the renewal period in calendar month as shown below:
<dx-alert infotype="explain" title="">
If cloud data disks are mounted to the instance, they will be renewed at the same time. You can also select **Align the data disk expiration time with that of the instance to xxxx** to align the instance's and cloud disk's expiration time.
</dx-alert>
![](https://qcloudimg.tencent-cloud.cn/raw/ea10aa12d48208169ef50fc9953318cb.png)
4. Click **OK** to enter the renewal order payment page, click **Submit order**, and make the payment as prompted.


#### Batch renewing instances
1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/).
2. Click **Fees** in the top-right corner and click **Renew** in the drop-down list box.
3. On the renewal management page, select the target instances and click **Batch renewal** above the list as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/cfd65f92e6a20885d021f3a9feb7e434.png)
4. In the **Batch Renewal** pop-up window, select the renewal period, click **OK**, and make the payment for the renewal order.

:::
::: Renewing to-be-repossessed instances[](id:recycled)

#### Renewing one instance
1. On the **Instances** page, find the target instance.
2. In the instance card in the instances list, select **More** > **Renew** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/aaf8b3f5c689209f05ace722158736fe.png)
3. In the **Renew instance** pop-up window, select the renewal period and click **OK**.


#### Batch renewing instances
1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/).
2. Click **Fees** in the top-right corner and click **Renew** in the drop-down list box.
3. On the renewal management page, select the target instances and click **Batch renewal** above the list as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/cfd65f92e6a20885d021f3a9feb7e434.png)
4. In the **Batch Renewal** pop-up window, select the renewal period, click **OK**, and make the payment for the renewal order.


:::
</dx-tabs>



### Auto-Renewal

<dx-alert infotype="explain" title="">
You can select **Auto-renew the device every month if my account has sufficient balance** during [instance purchase](https://intl.cloud.tencent.com/document/product/1103/41404) to enable the auto-renewal feature. After successfully creating an instance, you can modify its auto-renewal settings in the following steps:
</dx-alert>




Choose the appropriate operation method based on your actual needs: 
<dx-tabs>
::: Setting auto-renewal for one instance
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. In the instance list, select the target instance to enter its details page.
3. In the **Billing information** section, you can **enable** or **disable** the instance auto-renewal feature as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/72be090b1890ea787c370c7a171ab583.png)
4. In the **Enable/Disable auto-renewal** pop-up window, click **OK**.

:::
::: Setting auto-renewal for multiple instances
1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/).
2. Click **Fees** in the top-right corner and click **Renew** in the drop-down list box.
3. On the renewal management page, select the target instances and click **Set to Auto-Renewal** above the list as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/6bbdd646b3a952e40d6df93571a98b03.png)
4. In the **Set to Auto-Renewal** pop-up window, click **OK**.
:::
</dx-tabs>


<dx-alert infotype="notice" title="">
- After auto-renewal is enabled, the instance will be automatically renewed on the expiration date. Make sure that your account balance is sufficient on the resource expiration date.
- If your instance expires today, manually renew it.</li>
- If you manually renew an instance before the expiration date, Tencent Cloud will automatically renew it on the latest expiration date.
- You can set auto-renewal, renew to a certain time, and perform other operations on the [renewal management page in the console](https://console.cloud.tencent.com/account/renewal).

</dx-alert>

