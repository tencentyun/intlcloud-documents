## Scenario
This document provides guidance on managing and purchasing spot instances. Currently, spot instances are available through the following channels:
- **CVM console**: **Spot Instances** has been added as an option to **Billing Mode** on the CVM purchase page.
- **BatchCompute console**: Spot instances can be selected when users submit jobs and create computing environments in the BatchCompute console.
- **TencentCloud API**: Parameters related to spot instances have been added to the [RunInstances API](https://intl.cloud.tencent.com/document/product/213/33237).


## Directions
### CVM console

1. Log in to the [CVM purchase page](https://buy.cloud.tencent.com/cvm).
2. On the **Select a model** tab page, set **Billing Mode** to **Spot Instances**.
3. Specify **Region**, **Availability Zone**, **Network**, **Instance**, and other configurations as required and prompted.
4. Check the information of the spot instance to be purchased and the cost details of each configuration item.
5. Click **Purchase** and complete payment.
After completing payment, you can log in to the [CVM console](https://console.cloud.tencent.com/cvm) to check your spot instance.

### BatchCompute console
- **Async API**: When you submit a job, create a computing environment, or modify the expected number of instances in a computing environment, the BatchCompute instance processes your requests asynchronously. When it cannot fulfill the current request due to inventory or price reasons, the BatchCompute instance continuously applies for spot instance resources until the current request is fulfilled.
If you need to release an instance, you need to adjust the expected number of instances in the computing environment via the BatchCompute console. If you release instances via the CVM console, the BatchCompute console will automatically create instances until the expected number of instances is met.
- **Cluster Mode**: The computing environment of a BatchCompute instance can maintain a batch of spot instances as a cluster. You only need to submit the expected quantity, configurations, and maximum price of the spot instances. The computing environment will continuously apply for spot instances until the expected quantity is met. Even if spot instances go offline, the computing environment will automatically apply for spot instances again to meet the expected quantity.
- **Fixed Price**: Currently, spot instances are provided at fixed discounts. You must set a value that is greater than or equal to the current market price. For the market prices, see [Spot Instances - Supported regions and instance types](https://intl.cloud.tencent.com/document/product/213/17817).

#### Directions

1. Log in to the [BatchCompute console](https://console.cloud.tencent.com/batch/env).
2. On the **Computing environment** page, randomly select a region, such as Guangzhou, and then click **New**.
The **New computing environment** page appears.
3. On the **New computing environment** page, set **Billing Type** to **Spot Instance** and then specify configurations such as **Model Type**, **Image**, **Name**, and **Expected quantity** as required, as shown in the following figure:
![](https://main.qcloudimg.com/raw/afb048292803098eeddd7c9ae6ede96a.png)
4. Click **OK** to finish creation.
Then you can check the new computing environment in the [BatchCompute console](https://console.cloud.tencent.com/batch/env). To view the creation progress of CVM instances that are being created in the computing environment, click **Activity Logs** and **Instance List** for the computing environment.


### TencentCloud API
In the RunInstances API, you can specify the [InstanceMarketOptionsRequest](https://intl.cloud.tencent.com/document/api/213/15753#InstanceMarketOptionsRequest) parameter to enable or disable the spot instance mode and configure the information about spot instances.
* **Sync API**: Currently, RunInstances provides a one-time synchronization request API. This means that if the application fails because the inventory is insufficient or the requested price is lower than the market price, the RunInstances API immediately returns a failure code and does not apply for the spot instance again.
* **Fixed Price**: Currently, spot instances are provided at fixed discounts. You must set a value that is greater than or equal to the current market price. For the market prices, see [Spot Instances - Supported regions and instance types](https://intl.cloud.tencent.com/document/product/213/17817).

#### Example
You have an instance in Guangzhou Zone 3, and the billing mode of the instance is pay-as-you-go on an hourly basis and in spot mode. The specific configurations of the billing mode are as follows:
- MaxPrice: 0.6 CNY/hour
- SpotInstanceType: one-time
- ImageId: img-pmqg1cw7
- InstanceType: S2.MEDIUM4 (Standard 2, 2-core, 4GB)
- InstanceCount: 1

#### Request parameters
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
&Placement.Zone=ap-guangzhou-3
&InstanceChargeType=SPOTPAID
&InstanceMarketOptions.MarketType=spot
&InstanceMarketOptions.SpotOptions.MaxPrice=0.60
&InstanceMarketOptions.SpotOptions.SpotInstanceType=one-time
&ImageId=img-pmqg1cw7
&InstanceType=S2.MEDIUM4
&InstanceCount=1
&<common request parameters>
```

#### Response parameters
```
{
  "Response": {
    "InstanceIdSet": [
      "ins-1vogaxgk"
    ],
    "RequestID": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```
