## Images
A Tencent Cloud image provides all the information needed to start a CVM instance. After specifying the desired image, you can start as many instances as you want from the image. You can also start instances from as many different images as you need. Generally speaking, an image is the "installation disk" of a CVM instance.

## Image Types
Tencent Cloud provides the following types of images:
- **Public image**: Available to all users and cover major operating systems.
- **Custom image**: Only available to the creator and the users with whom the image is shared. A custom image is created from running instances or imported from external sources.
- **Shared image**: Shared by other users. They can only be used to create instances.

For more information on image types, see [Image Types](https://intl.cloud.tencent.com/document/product/213/4941).

## Image Billing[](id:mirrorBilling)
Using images incur fees. The fees for each image type are as described below:
<table>
<tr>
<th width="16%">Image Type</th><th>Description</th>
</tr>
<tr>
<td>Public image</td>
<td>Windows images in regions outside the Chinese mainland are charged. All other images are free of usage.</td>
</tr>
<tr>
<td>Custom image</td>
<td>
Images use the CBS snapshot service for data storage:
<ul style="margin:0px">
<li>A free tier of 50 GB is provided in the Chinese mainland. For more information, see <a href="https://intl.cloud.tencent.com/document/product/362/32415">Billing Overview</a>.</li>
<li>Retaining custom images incurs fees. For more information, see <a href="https://intl.cloud.tencent.com/document/product/362/32415">Billing Overview</a>.</li>
</ul>
</td>
</tr>
<tr>
<td>Shared image</td>
<td>Shared images are custom images shared to other Tencent Cloud accounts. The target accounts will not be charged. Retaining custom images incurs snapshot fees for the source account. For more information, see <a href="https://intl.cloud.tencent.com/document/product/362/32415">Billing Overview</a>.</td>
</tr>
</table>

## Use Cases
 - **Deploy a specific software environment**
You can use all types of images to quickly set up an environment with the specific software.  
 - **Deploy software environments in batches**
By creating an image of a CVM instance, you can create multiple CVM instances with the same environment by choosing the image as the OS.
 - **Back up a server runtime environment**
You can create an image of a CVM instance to back up the running environment. If the CVM instance ceases to run properly because its software environment is damaged, this image can be used to recover the environment.

## Custom Image Lifecycle

After creating or importing a custom image, you can use it to launch new instances. The diagram below shows the lifecycle of a custom image.
![](http://mc.qcloudimg.com/static/img/b11a8e644fd89ce844c8fb0b69e7044a/image.png)

