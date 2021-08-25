## Overview

This document describes how to use the resource management feature to quickly deliver resources to devices or upload device resources to the IoT Hub platform.


[](id:test)
## Platform Resources

The platform resource feature allows you to deliver resources uploaded to the IoT Hub platform to devices.


### Adding resource

1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iothub), click **Resources** on the left sidebar, and select **Platform Resources** to enter the resource list page and view all uploaded resources currently on the platform.
2. Click **Add Resource** to add a resource by entering the resource information.

	 - Resource Name: it can contain up to 32 letters, digits, underscores, minus signs, and parentheses and must begin with a letter or digit.
	 - Product: select the product of the resource to be uploaded.
	 - Resource: the resource file to be uploaded cannot exceed 1,024 MB in size.
	 - Resource Description: it is the description and record of the resource to be uploaded and can contain 0–100 characters.
3. After successful upload, click **Save**, and the added resource will be displayed in the list. You can perform operations such as delivering, adding, deleting, querying, and modifying the resource and viewing its details.

>?You can upload up to 1,000 pieces or 1 GB of resource files under each account. If the limit is exceeded, please delete some old resources first.
>

### Delivering resource

Select the resource to be delivered and click **Deliver Resource** on the right of the resource list to initiate a delivery task.
![](https://main.qcloudimg.com/raw/98c2bbecc1b85cf9f9a9429fc69a16d9.png)
Resources can be delivered to a single device or batch delivered to multiple devices as detailed below:
<dx-tabs>
::: Delivery to one device
1. Go to the resource delivery page, select **Single Device**, and select the target device for delivery in the drop-down list.

2. Click **Save**, and the system will perform the delivery task by delivering the selected resource to the selected target device.
:::
::: Batch delivery to multiple devices
1. Go to the resource delivery page, select **Multiple Devices**, and upload the list of target devices.

2. Click **Download Template** to get the template file, enter the correct `DeviceName` values in the template, and click **Browse** to upload it. Up to 10,000 devices can be uploaded at a time, and only CSV files are supported.
3. Click **Save**, and the system will perform the delivery task by delivering the resource to the target devices.
:::
</dx-tabs>


### Viewing resource details

1. In the resource list, click **View Details** on the right to view the resource details.
   ![](https://main.qcloudimg.com/raw/b5d9ffa95cf937ca4ad29ab647c2a368.png)
2. On the resource details page, you can view the resource details, statistics of devices to which the resource has been delivered, and delivery task management list.
![](https://main.qcloudimg.com/raw/91e18ad68b9ef4fa2eac390b5cdd1666.png)
 - Resource Information: it includes the resource name, resource signature, signature algorithm, adding time, and resource description.
 - Delivery Statistics: it includes the total number of devices in the resource delivery task and the numbers of devices in different delivery status.
 - Task management list:
    - Click **Tasks** to view all delivery tasks of this resource. There are four delivery task status: not started, creating, created, and creation failed.
     ![](https://main.qcloudimg.com/raw/44f4178eda0bb682bcee5e21286dd935.png)
    - Click **Devices** to view the detailed records of devices in all delivery tasks of this resource. There are five device delivery status: to be pushed, pushed, delivering, delivered, and delivery failed.
     ![](https://main.qcloudimg.com/raw/e6fb2a5298bae7fe1a7a54bec8de7bf1.png)
3. In **Tasks** or **Devices** in task management, click **View Details** on the right of a task to enter the task details page, where you can view the list of target devices, delivery status, and numbers of devices in different delivery status in this task. 
   ![](https://main.qcloudimg.com/raw/f14feb0dfb2b7c32debedb467fe8f48f.png)

In the device details list, you can view the current delivery status and status details of all target devices in the delivery task.
- If the delivery status is **To push** or **Pushed**, no status details will be displayed.
- If the delivery status is **Delivering**, the status details will display **Delivering** and the delivery progress values in percentage of each device.
- If the delivery status is **Delivery failed**, the status details will display the error messages.

In addition, you can cancel or retry resource delivery on the right of the device details list based on the delivery progress. Devices to which delivery is canceled will be marked as **Delivery failed**. For such devices, you can click **Retry** to deliver the resource again.

## Device Resource

The device resource feature allows you to directly download and view resources uploaded by devices to the platform in the console.

### Directions

1. A device uploads its resource to the platform over the [resource upload](https://intl.cloud.tencent.com/document/product/1105/41509) communication protocol. After successful upload, the resource will be displayed in the resource list in the IoT Hub console.
3. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iothub), click **Resources** on the left sidebar, select **Device Resources** to enter the resource list page, where you can view all resources uploaded by devices and perform operations such as downloading and deleting resources.
   ![](https://main.qcloudimg.com/raw/033c18a78c6b11430c84f2da8688cea5.png)






