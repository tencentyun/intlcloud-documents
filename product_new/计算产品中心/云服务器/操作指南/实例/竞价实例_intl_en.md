There are two ways to use spot instances.
**TencentCloud API** 
You can find parameters related to spot instances in [CVM RunInstance API](https://intl.cloud.tencent.com/document/api/213/15730).
* **Batch Compute Console** 
Now you can select spot instances when submitting jobs and creating a computing environment in the Batch Compute console.

## TencentCloud API
[InstanceMarketOptionsRequest](https://intl.cloud.tencent.com/document/api/213/15753#InstanceMarketOptionsRequest), a parameter in RunInstance API can specify the use of the spot instance mode and make related configuration.
![](https://main.qcloudimg.com/raw/e574f19520d5cdf2c6583d0314b904a9.png)
![](https://main.qcloudimg.com/raw/725e818693620acae191c9e6a4dfdb9d.png)

* **Sync API**: Currently RunInstance provides a one-time sync request API, which means that if the application fails due to insufficient supply or request price lower than market price, it will immediately return failure, and will not apply again.
* ** Fixed price (beta testing)**: Fixed discount mode is used during the beta testing period, so you must set the parameter to greater than or equal to the current market price. For detailed market prices, see [Spot Instance - Supported Regions and Types](https: //intl.cloud.tencent.com/doc/product/213/17817).

## TencentCloud API Example
#### Use Case
Region of the instance: Guangzhou Zone 3; billing mode: hourly pay as you go; highest bid price: $0.6/hour; bid request mode: one-time request; image ID: img-pmqg1cw7; selected model: S2.MEDIUM4 (Standard S2, 2-core, 4 GB); quantity: 1.

#### Request Parameters
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
&<Common request parameter>
```

#### Response Parameters
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

## Batch Compute Console
* **Async API**: When you submit a job, create a computing environment, or modify the expected number of computing environments, Batch Compute will process your request asynchronously. That means if the current request cannot be fulfilled due to factors such as inventory and price, Batch Compute will continue to apply for spot instance resources until the request is fulfilled. Therefore, before you release instances, you need to first change the number of computing environment instances via the Batch Compute console; otherwise, after you release instances in the CVM console, Batch Compute will automatically create new instances until the expected number is met.
* **Cluster mode**: The computing environment of Batch Compute supports maintaining a batch of spot instances as a cluster. You only need to submit the desired quantity, configuration and highest bid. The computing environment will automatically and continuously initiate requests until the desired quantity is met. Even if there is an interruption, Batch Compute will automatically make applications again.
* ** Fixed price (beta testing)**: Like the price used in TencentCloud API, the price must be higher than or equal to the current market price.

### Directions 

#### I. Go to the Batch Compute Console
![](https://main.qcloudimg.com/raw/fe2224004fa89a3a9e18e8b264fb2dff.png)

Go to the [Batch Compute Console](https://console.cloud.tencent.com/batch/env).

#### II. Go to Computing Environment
Click **New** to enter the computing environment creation page.

![](https://main.qcloudimg.com/raw/afb048292803098eeddd7c9ae6ede96a.png)

Verify that you are on the whitelist for using spot instances: select an availability zone that supports spot instances, such as Guangzhou zone 3. If you can see the **Spot Instance** option in the drop-down menu shown in the figure above, it means that you are on the whitelist; otherwise, please submit an application for using spot instances first.

#### III. Create Computing Environment with Spot Instance

![](https://main.qcloudimg.com/raw/0b6393888c46beb444ba4c3418c9dad0.png)

Select **Spot Instance** type, and select the model, image, name, number of expected instances, etc. you need, click **OK**.

#### IV. View the New Computing Environment

![](https://main.qcloudimg.com/raw/e98a5dd699db624c96d4292b1ab29d30.png)

After you finish the creation, go back to the [Batch Compute Console] (https://console.cloud.tencent.com/batch/env), you will see the new computing environment and CVMs being created in it. You can go to **Activity Log** and **Instance List**  to check the creating progress.
