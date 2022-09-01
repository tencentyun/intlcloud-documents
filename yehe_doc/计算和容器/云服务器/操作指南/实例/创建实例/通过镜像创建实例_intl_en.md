## Overview
You can use a custom image to create CVM instances of the same operating system, applications, and data to improve efficiency. This document guides you through how to create an instance using a custom image.


## Preparations
You must have a custom image under your account and in the region where you want to create an instance.
If there is no custom image, see the following solutions:
<table>
	<tr><th>Image Status</th><th>Solution</th></tr>
	<tr><td>Images on local computers or other platforms</td><td>Import the system disk image on local computers or other platforms to the custom image on CVM. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4945">Overview</a>.</td></tr>
	<tr><td>There are template instances but no custom images</td><td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4942">Creating Custom Images</a>.</td></tr>
	<tr><td>Custom images in other regions</td><td>Copy the custom image to the target region where you want to create an instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4943">Copying Images</a>.</td></tr>
	<tr><td>Custom images under another account</td><td>Share the custom image with the account under which you want to create an instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4944">Sharing Custom Images</a>.</td></tr>
</table>

## Directions

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. Click **Image** on the left sidebar to enter the image management page.
3. Select a region at the top of the **Image** page.
4. Select a tab based on the image source to view its image list.
 - **Public Image**: Go to the public image page.
 - **Custom Image**: Go to the custom image page.
 - **Shared Image**: Go to the shared image page.
5. In the **Operation** column of the target image, click **Create Instance**.
![](https://main.qcloudimg.com/raw/4c5806f49da53595d31ad07662bf363a.png)
6. In the pop-up window, click **OK**.
7. Configure and create the instance as prompted by the page.
The **Region** and **Image** fields are automatically filled. Complete the other configurations of the instance as needed. For more information, see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
<dx-alert infotype="explain" title="">
If you use a custom image that contains one or more data disk snapshots, the system will automatically create the same quantity of cloud disks as data disks and the same capacity as each snapshot. You can increase, but cannot reduce, the cloud disk capacity.
</dx-alert>



## References
You can also call the [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237) API to create an instance by using a custom image.


<dx-alert infotype="explain" title="">
If you use an image of the entire CVM instance to create an instance, call the [DescribeImages](https://intl.cloud.tencent.com/document/product/213/33272) API to get the snapshot ID associated with the image first and then call the `RunInstances` API to pass in the snapshot ID parameter; otherwise, the created cloud disk cannot match the snapshot ID, the snapshot data cannot be rolled back, the data disk has no data, and mounting cannot be performed.
</dx-alert>
