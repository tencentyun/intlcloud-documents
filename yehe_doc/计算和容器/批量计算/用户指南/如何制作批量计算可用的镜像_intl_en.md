## Overview

BatchCompute relies on Cloud-init service to initialize Cloud Virtual Machines (CVM). For this reason, when BatchCompute is used, the image that is entered must already have Cloud-init installed and configured. Otherwise, the job executions and CVM creation in compute environments may fail.

(Cloud-init provides the ability to customize the configuration of the CVM instance when it is first initialized.)

To install and configure Cloud-init, follow the steps below:
* ```New``` Linux CVM/custom images: all current versions of Tencent Cloud CentOS and Ubuntu public images support Cloud-init by default. When you create CVM instances and custom images from these public images, you do not need to manually install and configure Cloud-init.
* ``Existing`` Linux CVM/custom images: for CVM instances or custom images created previously, you need to manually install Cloud-init as instructed in [Installing cloud-init on Linux ](https://intl.cloud.tencent.com/document/product/213/12587).
* Windows: you must use an image from the Tencent Cloud Image Market to create a CVM instance or make a custom image.

Common operating system images that already contain Cloud-init are as follows:
* img-31tjrtph (CentOS 7.2 64-bit)
* img-er9shcln (Windows Server 2012 R2 Standard Edition 64-bit Chinese)
* img-pyqx34y1 (Ubuntu Server 16.04.1 LTS 64-bit)








