## What Is an Image?
An image is a serialized copy of the entire state of a computer system stored as a file. You can consider an image to be a system installation disk. It contains everything you need to launch a CVM instance. An image can launch as many CVM instances as you want, and you can launch CVM instances from as many images as you want. 

## Image Types
Tencent Cloud provides the following types of images:
- **Public images**: available to all users and cover most mainstream operating systems.
- **Custom images**: only available to the owner and the users with whom the images are shared. Custom images are created from instances or imported from external sources.
- **Shared images**: shared by other users. These can only be used to create instances.

For more information on image types, please see [Image Types](https://intl.cloud.tencent.com/document/product/213/4941).

## Use Cases
 - **Deploy a specific software environment**
To provide web services or develop applications, you often require a specific set of software running in a cohesive environment. Building such environments and installing software are time-consuming and complex, which is why Tencent Cloud is perfect for such tasks. Custom images and shared images can help you satisfy your requirements quickly and effortlessly.
 - **Deploy software environment in batches**
You can create an image from an instance with a deployed environment and then use the image to create instances in batches. After creation, these instances will have the same software environment as the original instance.
 - **Server runtime environment backup**
You can make a custom image from a CVM instance to back up the runtime environment. If the environment is corrupted afterwards, you can use the image to restore it. 

## Image Lifecycle

The following illustrates the lifecycle of a custom image. After the custom image is created or imported, you can use it to launch a CVM instance. Custom images can be copied to other regions under the same account. You can also share custom images with other users.
![](http://mc.qcloudimg.com/static/img/b11a8e644fd89ce844c8fb0b69e7044a/image.png)


