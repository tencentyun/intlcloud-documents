### Operations Guide for RIs

Currently, RIs can be created and used only through APIs.

1. View the RIs that you can purchase. For more information, see the document of the [purchasable RI listing API](http://10.198.144.46/document/product/213/32751?!document=1&!preview)

2. Purchase RIs. For more information, see the document of the [RI purchasing API](http://10.198.144.46/document/product/213/32750?!document=1&!preview)

3. View the RIs that you have purchased. For more information, see the document of the [purchased RI listing API](http://10.198.144.46/document/product/213/32752?!document=1&!preview)

4. Purchase on-demand instances that have exactly the same attributes as the RIs. For more information, see the document of the [instance creating API](https://cloud.tencent.com/document/product/213/15730) or log in to the console

   > Note: RIs will be matched with on-demand instances with exactly the same attributes created before or after the RIs take effect

#### Steps

Example: Buy two Linux RIs of model S3.16XLARGE256 in Silicon Valley Zone 1

> The information such as availability zone, model, and OS shown in the example is for reference only. For more information about RIs that you can actually purchase, query by calling the [purchasable RI listing API](http://10.198.144.46/document/product/213/32751?!document=1&!preview)

#### Viewing Purchasable RIs (DescribeReservedInstancesOfferings)

> If the RI configuration ID is known, you can use the RI purchasing API to purchase RIs directly

Get the RI configuration ID (ReservedInstancesOfferingId)

Input parameters:

![1](https://main.qcloudimg.com/raw/d415f09aecc07c2c522f3c560e7d7f87.jpg)

Output parameters: ![2](https://main.qcloudimg.com/raw/e0f0a6c859bd445cd1340f73fe005a53.jpg)

#### Purchasing RIs (PurchaseReservedInstancesOffering)

RI configuration items ID=149d1ebe-7c8c-XXXX-XXXX-XXXXXXXXXX and InstanceCount=2 are used as input parameters for the RI purchasing API

Input parameters:

![3](https://main.qcloudimg.com/raw/79b582cf64d02612c644a8ca36d0d931.jpg)

Output parameters:

![4](https://main.qcloudimg.com/raw/15ae128ddd454c393b881af487dd20c5.jpg)

#### Viewing Purchased RIs (DescribeReservedInstances)

Enter the relevant criteria for the RIs that you want to view, such as Silicon Valley region, S3.16XLARGE256, and Linux, and information of the purchased RIs matching the entered criteria will be obtained

Input parameters:

![5](https://main.qcloudimg.com/raw/cd5e3feeb79bce7874d6da1b229eda0a.jpg)

Output parameters:

![6](https://main.qcloudimg.com/raw/2cc7c8fac0f23ebcfc48c402d19d0570.jpg)

#### Purchasing On-demand Instances with the Same Attributes (RunInstances)

Purchase an on-demand instance with the same attributes as the RI, i.e., a Linux on-demand instance of model S3.16XLARGE256 in Silicon Valley Zone 1.

Input parameters:

![7](https://main.qcloudimg.com/raw/8e01b4a37970fe4cde08f98e4c3a180a.jpg)

Output parameters:

![8](https://main.qcloudimg.com/raw/a0b71f794d1828e70d0cbe4f1c081f0a.jpg)
