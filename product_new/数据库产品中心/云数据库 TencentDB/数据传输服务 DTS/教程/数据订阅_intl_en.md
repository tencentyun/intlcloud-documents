## 1. Feature description
DTS provides a binlog-based incremental data subscription feature that allows you to subscribe to incrementally updated data in TencentDB in just a few steps:
* Purchase and create a subscription channel for your TencentDB instance in the DTS Console.
* Use the DTS data subscription SDK to connect to this subscription channel, so as to subscribe to and consume incremental data.


## 2. Create a data subscription channel
Log in to the DTS Console and enter the data subscription page.
* Click **Create Subscription** in the top-right corner to configure a subscription channel.
![][img-1]
* Select the region where the source TencentDB instance resides.
![][img-2]
* Once the channel is created, return to the console and complete initial configuration for it.
![][img-3]
* Select the source TencentDB instance.
![][img-4]
* Select your desired data sync type and table to be synced.
![][img-5]
	The granularity for subscribed objects in DTS includes database level and table level, i.e., you can choose to subscribe to certain databases or tables.
	DTS offers two data subscription modes: data update (DML) and structure update (DDL). In the first mode, you can only subscribe to three types of data changes caused by insertion/deletion/update. In the second mode, DTS pulls all structural changes in the entire TencentDB instance, and you need to filter out the desired data using the SDK.
* The subscription channel can be enabled after the subscribed object is selected.

## 3. Modify the consumption time point
 
DTS allows you to modify the consumption time point at any time during the consumption process. Once the modification is completed, the downstream SDK will begin pulling incremental data starting from the new consumption time point, which must be within the data range of the subscription channel. Currently, the consumption time point can only be modified in the DTS Console, but cannot be specified in the SDK.
You can modify the consumption time point in the following steps:
* Stop the SDK consumption process.

* Modify the consumption time point.
To modify the consumption time point, move your cursor over it to display the "Configure" button. Click the button to enter the modification page.

* Restart the SDK consumption process.
After the consumption time point is modified, you can restart the local SDK consumption process. Then, the SDK will begin subscribing to incremental data starting from the new consumption time point.

## 4. Modify the subscribed objects
DTS allows you to dynamically add/delete subscribed objects during the consumption process. If a subscribed object is added, the subscription channel will pull its incremental data starting from the current time. If a subscribed object is deleted, the SDK will no longer subscribe to its data.
You can modify the subscribed objects in the following steps:

* Entry for modifying subscribed objects:

* Modify the subscribed object.



## 5. Use the SDK to consume data
For more information, see [SDK User Guide](https://intl.cloud.tencent.com/document/product/571/8776).


[img-1]://main.qcloudimg.com/raw/9ad0b689799aee56054406c5cd67b4df.png
[img-2]://main.qcloudimg.com/raw/2eac1229584ab78be9802ea9254faf49.png
[img-3]://main.qcloudimg.com/raw/d25263473aabf08e4a145b6f59176510.png
[img-4]://main.qcloudimg.com/raw/081dc059e47109c6f4a236de38ea58fa.png
[img-5]://main.qcloudimg.com/raw/00cb11085e26b1ba7cabf034156bc39f.png
[img-6]://mc.qcloudimg.com/static/img/092b59bdade021f1c3d1ce0740161d62/6.png
[img-7]://mc.qcloudimg.com/static/img/f17f7720f13a33ed26b525dcd683046c/7.png
[img-8]://mc.qcloudimg.com/static/img/c86c4736a65766917a675b3def08883e/8.png
[img-9]://mc.qcloudimg.com/static/img/1ba4f66502db932c7066e8cbcc0da877/9.png
[img-10]://mc.qcloudimg.com/static/img/1602a9e4bf8a2e4668146d69e27dd940/10.png
[img-11]://mc.qcloudimg.com/static/img/1eb73f016d3bb7d0820ddf33a15e1569/11.png
[img-12]://mc.qcloudimg.com/static/img/c88d2d0ca2ec0b7cd29fade9262352ae/12.png
[img-13]://mc.qcloudimg.com/static/img/664293491411378f95bc238e620103d2/13.png
[img-14]://mc.qcloudimg.com/static/img/e7dc19b7a6918a8c1ef8e7a4b620d4d0/14.png
