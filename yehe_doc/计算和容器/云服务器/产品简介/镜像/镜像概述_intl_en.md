## Images
A Tencent Cloud image provides all the information needed to launch a CVM instance. With an image, you can launch instances with similar configurations easily. Generally speaking, an image is the "installation disk" of a CVM instance.

## Image Types
Tencent Cloud provides the following types of images:
- **Public image**: Available to all users and cover major operating systems.
- **Custom image**: Only available to the creator and the users with whom the image is shared. A custom image can be created from a running instance or imported from external sources.
- **Shared image**: Shared by other users. You can use shared images to create instances, but cannot modify the shared images.

For more information, see [Image Types](https://intl.cloud.tencent.com/document/product/213/4941).

## Image Billing[](id:mirrorBilling)
Check below for the billing details of images.
<table style="width:717px;">
<tr>
<th width="16%">Image Type</th><th>Description</th>
</tr>
<tr>
<td>Public image</td>
<td><ul style="margin:0px">
<li>For the usage of Windows images in regions outside the Chinese mainland, you are charged based on the instance specification.</li>
<li>Other public images are free of charge.</li>
</ul>
</td>
</tr>
<tr>
<td>Custom image</td>
<td>
The billing consists of the following two parts:
<ul style="margin:0px">
<li>Snapshot fee: The image use the CBS snapshot service. As a result, retaining custom images incurs a snapshot fee. For billing details of CBS service, see the <a href="https://intl.cloud.tencent.com/document/product/362/32415">Billing Overview</a>.</li>
<li>Image fee: If the custom image is sourced from paid images, using it incurs fees.</li>
</ul>
</td>
</tr>
<tr>
<td>Shared image</td>
<td>An shared image is a custom image shared to other Tencent Cloud accounts. If the shared image is sourced from paid images, using it incurs fees.</td>
</tr>
</table>



## Use Cases
 - **Deploy a specific software environment**
You can use all types of images to quickly set up an environment with the specific software.
 - **Deploy software environment in batch**
By creating an image of a CVM instance, you can create multiple CVM instances with the same environment by choosing the image as the OS.
 - **Back up a server runtime environment**
You can create an image of a CVM instance to back up the running environment. If the CVM instance ceases to run properly because its software environment is damaged, this image can be used to recover the environment.

## Custom Image Lifecycle

After creating or importing a custom image, you can use it to launch new instances. The diagram below shows the lifecycle of a custom image.
![](http://mc.qcloudimg.com/static/img/b11a8e644fd89ce844c8fb0b69e7044a/image.png)

