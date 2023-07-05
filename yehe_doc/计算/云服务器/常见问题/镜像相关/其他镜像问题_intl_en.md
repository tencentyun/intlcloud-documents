### What is an image?
An image is the template for CVM software configuration (operating systems, pre-installed programs, etc.). Tencent Cloud requires users to use images to launch instances. An image can launch multiple instances, and users can use it repeatedly. For more information on images, please see [Overview](https://intl.cloud.tencent.com/document/product/213/4940).

### What do I need to do before importing the image?
Before importing an image, you need to complete two major steps: applying for permissions and preparing image files. For more information, please see [Overview](https://intl.cloud.tencent.com/document/product/213/4945).

### How do I export an image for local testing?
Tencent Cloud Service Migration supports images in qcow2, vhd, raw, and vmdk formats.
You can use the image export tools of virtualization platforms such as VMWare vCenter Convert or Citrix XenConvert. For more information, please reference each platform’s export tool documentation. You can also export images [using Disk2vhd (Windows)](https://intl.cloud.tencent.com/document/product/213/17815) or [by running commands (Linux)](https://intl.cloud.tencent.com/document/product/213/17814).

### Can I delete a custom image that has been used to create a CVM instance?
Yes. After a custom image is deleted, it can no longer be used to launch a new CVM instance. It will not affect instances that have already been launched. If you want to delete all instances launched from this image, see [Reclaiming Instances](https://intl.cloud.tencent.com/document/product/213/4931) or [Terminating Instances](https://intl.cloud.tencent.com/document/product/213/4930).

### Can I delete a custom image that has been shared with another account?
No. You cannot delete a custom image that has been shared with another account. To delete it, you need to cancel image sharing first. For more information, see [Cancelling Image Sharing](https://intl.cloud.tencent.com/document/product/213/7148).


