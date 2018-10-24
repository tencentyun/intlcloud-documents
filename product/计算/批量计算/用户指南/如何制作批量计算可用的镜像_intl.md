## Summary

Batch relies on the Cloud-init service to initialize the CVM instance. Therefore, the image entered when using Batch must have successfully installed and configured Cloud-init; otherwise, the CVM instance creation will ``fail`` in the job execution or compute environment

(Cloud-init provides the ability to customize the configuration of the CVM instance when it is initialized for the first time)

Follow the guidelines below to install and configure Cloud-init
* ``New`` Linux-based CVM instance/custom image: At present, Tencent Cloud's CentOS and Ubuntu public images (all versions) support Cloud-init by default. When creating CVM instances and custom images based on these public images, you don't have to manually install and configure Cloud-init
* ``Existing`` Linux-based CVM instance/custom image: If it is a CVM instance or custom image created earlier, you need to manually install Cloud-init as described in [Installing cloud-init on Linux OS >>>](https://intl.cloud.tencent.com/document/product/213/12587)

The IDs of common operating system images that already contain Cloud-init are as follows:
* img-31tjrtph (CentOS 7.2 64-bit)
* img-pyqx34y1 (Ubuntu Server 16.04.1 LTS 64-bit)








