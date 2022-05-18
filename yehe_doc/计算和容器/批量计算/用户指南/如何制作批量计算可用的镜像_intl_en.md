## Overview

BatchCompute relies on Cloud-init service to initialize CVMs. Hence the image used for BatchCompute should have Cloud-init installed and configured. Otherwise, the job execution may fail, or CVMs cannot be created in the compute environment.

(With Cloud-init, you can customize the configuration of the CVM when it is first initialized.)

Note the following while installing and configuring Cloud-init:
* **Newly created** Linux CVM/image: all current versions of Tencent Cloud CentOS and Ubuntu public images support Cloud-init by default. When you create CVMs and custom images with these public images, you needn’t manually install and configure Cloud-init.
* **Existing** Linux CVM/image: if the CVMs or custom images are created earlier, you need to manually install Cloud-init. See [Installing Cloud-Init on Linux](https://intl.cloud.tencent.com/document/product/213/12587).
* Windows image: you need to create Windows CVMs and images via marketplace images. See [Windows Custom Images](https://intl.cloud.tencent.com/document/product/599/13035).

Common operating system images that already contain Cloud-init are as follows:
* img-31tjrtph (CentOS 7.2 64-bit)
* img-er9shcln (Windows Server 2012 R2 Standard 64-bit English)
* img-pyqx34y1 (Ubuntu Server 16.04.1 LTS 64-bit)









