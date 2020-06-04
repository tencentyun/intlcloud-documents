## Scenario
With a custom image, you create CVM instances of the same OS, applications and data more easily and efficiently. This topic guides you through how to create instances using a custom image.


## Prerequisites
You have custom images under your account and in the region where an instance needs to be created.
If there is no custom image, see the solutions given below:
<table>
	<tr><th>Image Status</th><th>Solution</th></tr>
	<tr><td>Image on local computers or other platforms</td><td>Import the system disk image on local computers or other platforms to the custom image on CVM. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4945">Overview</a>.</td></tr>
	<tr><td>No custom image, but template instances exist</td><td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4942">Creating Custom Images</a>.</td></tr>
	<tr><td>Custom images in other regions</td><td>Copy the custom image to the target region where an instance needs to be created. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4943">Copying Images</a>.</td></tr>
	<tr><td>Custom images under another account</td><td>Share the custom image with the account that needs to create an instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4944">Sharing Custom Images</a>.</td></tr>
</table>

## Directions

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. Click **Images** in the left sidebar to go to the **Image** page.
3. Select a region on the top of the **Image** page.
4. Select the tab based on the image source, and view the image list.
 - **Public Image**: go to the public image page.
 - **Custom Image**: go to the custom image page.
 - **Shared Image**: go to the shared image page.
5. Click **Create Instance** under the **Operation** column of the image to use.
![](https://main.qcloudimg.com/raw/4c5806f49da53595d31ad07662bf363a.png)
6. In the pop-up window, click **OK**.
7. Configure and create the instance as prompted by the page.
The **Region** and **Image** fields are automatically filled. Complete other configurations of the instance as needed. For more information, see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
> If you use a custom image that contains one or more data disk snapshots, Cloud Block Storage (CBS) will be created with the same quantity as snapshots and capacity as each snapshot. You may expand but cannot reduce the CBS capacity.
>

## Related documentation

You can also create a custom image using the RunInstances. For more information, see [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237)
