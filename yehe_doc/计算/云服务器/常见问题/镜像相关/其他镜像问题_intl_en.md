### What is an image?
An image is the template for CVM software configuration (operating systems, pre-installed programs, etc.). Tencent Cloud requires users to launch the instance using an image. An image can launch multiple instances, so users can use it repeatedly. For more information on images, please see [Overview](https://intl.cloud.tencent.com/document/product/213/4940).

### What do I need to do before importing the image?
Before importing an image, you need to complete two major steps: applying for permissions and preparing image files. For more information, please see [Overview](https://intl.cloud.tencent.com/document/product/213/4945).

### How do I export an image for local test?
Tencent Cloud Service Migration supports the image in qcow2, vhd, raw, and vmdk format.
You can use image export tools of virtualization platforms such as VMWare vCenter Convert or Citrix XenConvert by reference to the document of each platform. You can also export images [using Disk2vhd to export an image (Windows)](https://intl.cloud.tencent.com/document/product/213/17815) or [exporting an image by running commands](https://intl.cloud.tencent.com/document/product/213/17814).

### Can a custom image from which CVM instances created be deleted?
After a custom image is deleted, it can no longer be used to launch a new CVM instance, but will not affect instances that have already been launched. If you want to delete all instances launched from this image, see [Reclaiming Instances](https://intl.cloud.tencent.com/document/product/213/4931) or [Terminating Instances](https://intl.cloud.tencent.com/document/product/213/4930).

### Can I delete my custom image that has been shared with another account?
A custom image that has been shared with others cannot be deleted. To delete it, you need to cancel image sharing first. For more information, see [Cancelling Image Sharing](https://intl.cloud.tencent.com/document/product/213/7148).


