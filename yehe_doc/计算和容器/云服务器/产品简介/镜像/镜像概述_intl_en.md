## Concept
A Tencent Cloud image provides all the information needed to launch a CVM instance. With an image, you can launch instances with similar configurations easily. Generally speaking, an image is the "installation disk" of a CVM instance.

## Image Types
Tencent Cloud provides the following types of images:
- **Public image**: Available to all users and cover major operating systems.
- **Custom image**: Only available to the creator and the users with whom the image is shared. A custom image can be created from a running instance or imported from external sources.
- **Shared image**: Shared by other users. You can use shared images to create instances, but cannot modify the shared images.

For more information, see [Image Types](https://intl.cloud.tencent.com/document/product/213/4941).

## Image Billing[](id:mirrorBilling)
For billing details of images, see [Billing Overview](https://intl.cloud.tencent.com/document/product/213/2179).

## Deployment with Images vs Manual Deployment

<table style="width:717px;">
<thead>
<tr>
<th style="width:85px;height:45px;position:relative;font-weight:700;" valign="top"><div style="position:absolute;width:1px;height:102px;top:0;left:0;background-color: #d9d9d9;transform: rotate(-55deg);transform-origin:top;"></div><div style="position:relative;left:30px">Mode</div><div style="position:relative;left:-10px">Item</th>
<th><strong>Deployment with Images</strong></th>
<th><strong>Manual Deployment</strong></th>
</tr>
</thead>
<tbody><tr>
<td>Deployment duration</td>
<td>3 to 5 minutes</td>
<td>1 to 2 days</td>
</tr>
<tr>
<td>Deployment process</td>
<td>Quickly create a suitable CVM based on mature marketplace solutions or the already used solutions.</td>
<td>Select the appropriate operating system, database, application software and plugins to create a CVM, and installation and debugging is required.</td>
</tr>
<tr>
<td>Security</td>
<td>Public images and custom images have been tested and audited by Tencent Cloud. The sources of shared images need to be identified by users.</td>
<td>It depends on the development and deployment personnel.</td>
</tr>
<tr>
<td>Applicable scenarios</td>
<td>Public images: Genuine operating systems, which contain the initialized add-ons provided by Tencent Cloud.<br>Custom images: Quickly create the same software environment as an existing CVM, or perform environment backup.<br>Shared images: Quickly create the same software environment as other users' CVMs.</td>
<td>Configure a CVM completely by yourself, without basic settings provided.</td>
</tr>
</tbody></table>

## Use Cases
 - **Deploy a specific software environment**
You can use shared images and custom images to quickly set up an environment with the specific software.
 - **Deploy software environment in batch**
By creating an image of a CVM instance, you can create multiple CVM instances with the same environment by choosing the image as the OS.
 - **Back up a server runtime environment**
You can create an image of a CVM instance to back up the running environment. If the CVM instance ceases to run properly because its software environment is damaged, this image can be used to recover the environment.

## Custom Image Lifecycle

After creating or importing a custom image, you can use it to launch new instances. The diagram below shows the lifecycle of a custom image.
![](https://qcloudimg.tencent-cloud.cn/raw/fc696f071652956e00c62c273fc5dde3.png)

