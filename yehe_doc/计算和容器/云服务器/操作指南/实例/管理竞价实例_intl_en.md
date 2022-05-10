## Overview
This document provides guidance on managing and purchasing spot instances. Currently, spot instances are available through the following channels:
- **CVM console**: **Spot Instances** has been added as an option to **Billing Mode** on the CVM purchase page.
- **BatchCompute console**: Spot instances can be selected when users submit jobs and create computing environments in the BatchCompute console.
- **TencentCloud API**: spot instance parameters have been added to the [RunInstance API](https://intl.cloud.tencent.com/zh/document/product/213/33237).


## Directions
<dx-tabs>
::: CVM console

1. Log in to the [CVM instance purchase page](https://buy.intl.cloud.tencent.com/cvm?regionId=1&projectId=-1).
2. On the **Select Model** tab, set **Billing Mode** to **Spot Instances** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/1c6720cefc4f56bc05d7ba7fc7c31347.png)
3. Select region, availability zone, network type, instance and other configuration information as needed and prompted by the page.
4. Check the information of the spot instance to be purchased and the cost details of each configuration item.
5. Click **Activate** and make the payment.
After completing payment, you can log in to the [CVM console](https://console.cloud.tencent.com/cvm) to check your spot instance.

:::
::: BatchCompute console
### BatchCompute feature description
- **Async API**
When you submit a job, create a computing environment, or modify the expected number of instances in a computing environment, your BatchCompute instance will process your request asynchronously. When it cannot fulfill the current request due to inventory or price reasons, the BatchCompute instance will continuously apply for spot instance resources until the current request is fulfilled.
If you need to release an instance, you need to adjust the expected number of instances in the computing environment via the BatchCompute console. If you release instances via the CVM console, the BatchCompute console will automatically create instances until the expected number of instances is met.
- **Cluster mode**
The computing environment of a BatchCompute instance can maintain a batch of spot instances as a cluster. You only need to submit the desired quantity, configuration, and maximum price of the spot instances, and the computing environment will automatically and continuously apply for spot instances until the expected quantity is reached. Even if spot instances go offline, the computing environment will automatically apply for spot instances again to reach the expected quantity.
- **Fixed price**
The fixed discount mode is used currently, so you must set the parameter to a value greater than or equal to the current market price. For more information on the market prices, see [Spot Instance](https://intl.cloud.tencent.com/document/product/213/17817).

### Directions
1. Log in to the [BatchCompute console](https://console.cloud.tencent.com/batch/env).
2. On the computing environment management page, randomly select a region, such as Guangzhou, and then click **Create**.
The **Create Computing Environment** page appears.
3. On the **Create Computing Environment** page, set **Billing Type** to **Spot Instance** and then configure information such as **Model**, **Image**, **Name**, and **Expected Quantity** as needed as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/95437ac5e26f3270c758fcc282042972.png)
4. Click **OK**.
Then you can view the new computing environment in the [BatchCompute console](https://console.cloud.tencent.com/batch/env). To view the creation progress of CVM instances that are being created in the computing environment, click **Activity Log** and **Instance List** for the computing environment.
:::
::: TencentCloud API
In the `RunInstance` API, you can specify the [InstanceMarketOptionsRequest](https://intl.cloud.tencent.com/zh/document/api/213/15753?from_cn_redirect=1) parameter to enable or disable the spot instance mode and configure the information about spot instances.
* **Sync API**: currently, `RunInstance` provides a one-time sync request API. This means that if the application fails because the inventory is insufficient or the requested price is lower than the market price, the `RunInstance` API will immediately return a failure code and no longer apply for the spot instance again.
* **Fixed price**: the fixed discount mode is used currently, so you must set the parameter to a value greater than or equal to the current market price. For more information on the market prices, see [Spot Instance](https://intl.cloud.tencent.com/document/product/213/17817).

### Sample scenario description
You have an instance in Guangzhou Zone 3, and the billing mode of the instance is pay-as-you-go on an hourly basis and in spot mode. The specific configurations of the billing mode are as follows:
- MaxPrice: 0.0923 USD/hour
- SpotInstanceType: one-time
- ImageId: img-pmqg1cw7
- InstanceType: S2.MEDIUM4 (Standard 2, 2-core, 4GB)
- InstanceCount: 1

### Request parameters
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
&Placement.Zone=ap-guangzhou-3
&InstanceChargeType=SPOTPAID
&InstanceMarketOptions.MarketType=spot
&InstanceMarketOptions.SpotOptions.MaxPrice=0.0923
&InstanceMarketOptions.SpotOptions.SpotInstanceType=one-time
&ImageId=img-pmqg1cw7
&InstanceType=S2.MEDIUM4
&InstanceCount=1
&<Common request parameters>
```

### Response parameters
```
{
  "Response": {
    "InstanceIdSet": [
      "ins-1vogaxgk"
    ],
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```
:::
</dx-tabs>
