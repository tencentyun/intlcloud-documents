The **CVM purchase page** will be available soon and will feature a spot instance selection entry in addition to the pay-as-you-go instance one.
**During the beta test**, you need to first submit an [application](https://cloud.tencent.com/apply/p/rid926tmuie). After the application approval, you can view and use spot instances via TencentCloud API and console.
Currently, there are two spot instances usage methods.
* **TencentCloud API** 
Spot instance related parameters were added to the [CVM RunInstance API](/document/api/213/15730).
* **BatchCompute Console** 
BatchCompute now supports spot instances selection when submitting jobs and creating compute environment.

## TencentCloud API
The parameter [InstanceMarketOptionsRequest](https://cloud.tencent.com/document/api/213/15753#InstanceMarketOptionsRequest) in the RunInstance API can specify the use of spot instance mode and configure relevant information.
![](https://main.qcloudimg.com/raw/8e3dc464e202ed3355b6bb3b4fe72566.png)
![](https://main.qcloudimg.com/raw/281df8c2b655876f612c8ae34f1e2951.png)
* **Sync API**: Currently, RunInstance provides a one-time sync request API, which will return a failure immediately if the application fails (due to insufficient inventory or application price lower than market price) and will not apply again.
* **Fixed price (in public trial)**: Fixed discount mode is used during the public trial, so you have to set the parameter to be greater than or equal to the current market price. For detailed market prices, see [Spot Instance - Supported Regions and Types](/doc/ Product/213/17817).

### TencentCloud API Example
#### Scenario Description
The instance is located in Guangzhou Zone 3, the billing mode is pay-as-you-go on an hourly basis, the highest bid is RMB0.6/hour, the bid request mode is one-time request, the image ID is img-pmqg1cw7, the selected model is 2C4G II Standard (S2.MEDIUM4), and the number of purchased instances is 1.

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

#### Return Parameters
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

## BatchCompute Console
* **Async API**: When your submit a job, create a compute environment or modify the desired number of compute environments, BatchCompute will process your request asynchronously, that is, if the current request cannot be satisfied due to reasons such as inventory and price, it will retry applying for spot instance resources until the request is fulfilled. (Therefore, when you need to release instances, you need to adjust the number of compute environment instances in the BatchCompute console. If the instances are released in the CVM console, BatchCompute will automatically create instances again until the desired quantity is met.)
* **Cluster mode**: The compute environment of BatchCompute supports maintaining a batch of spot instances in cluster mode. You only need to submit the required quantity, specifications and highest bid, and the compute environment will automatically keep applying until the desired quantity is met. Even if an interruption occurs, the application will be automatically re-initiated to fulfill the quantity.
* **Fixed price (public trial)**: Just like TencentCloud API, the price must be greater than or equal to the current market price.

### BatchCompute Console Usage Steps

#### I. Open the BatchCompute console
![](https://main.qcloudimg.com/raw/77c64f7632e04183d598bbb8af9211cd.jpg)

First, go to the [BatchCompute console](https://console.cloud.tencent.com/batch/env).

#### II. Create a compute environment
Click **Create** to enter the compute environment creating page.

![](https://main.qcloudimg.com/raw/84c0019c5f2cd090a829f2bd35f06d03.jpg)

Confirm that you are eligible for spot instance: Select any availability zone that supports spot instance (e.g., Guangzhou Zone 3), and if you can see the **Spot instance** option in the drop-down menu as shown in the figure, it means that you are in the whitelist. Otherwise, please submit an application first and wait for approval.

#### III. Create a spot instance-enabled compute environment

![](https://main.qcloudimg.com/raw/f9db70d48dedf80f4977efb88c008f60.jpg)

Select the **Spot instance** type, select the model, image, name and desired number of instances and click **OK**.

#### IV. View the created compute environment

![](https://main.qcloudimg.com/raw/086852467032fa4cf9e209e4afe86c96.jpg)

After the creation is completed, you will be redirected back to the [BatchCompute console](https://console.cloud.tencent.com/batch/env), where you can view the compute environment just created. The CVMs in the compute environment are also created synchronously, which you can view in **Event log** and **Instance list**.
