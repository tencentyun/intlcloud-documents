In addition to [create custom images](https://intl.cloud.tencent.com/document/product/213/4942), Tencent Cloud also allows you to import images. You can import an image file of a server system disk on the local machine or another platform into CVM custom images. After the image is imported, you can use it to create a CVM or reinstall the system of an existing CVM.

<span id="preparations for import"></span>
## Prepare to import

You need to prepare in advance an image file that meets the import requirements.
- **Requirements for Linux images:**
<table>
<tr><th>Image Attribute</th><th>Condition</th></tr>
<tr><td>Operating System</td><td><ul><li>CentOS, Ubuntu, Debian, CoreOS, OpenSUSE, and SUSE</li><li>32-bit and 64-bit are supported</li></ul></td></tr>
<tr><td>Image Format</td><td><ul><li>RAW, VHD, QCOW2 and VMDK are supported</li><li>Use<code>qemu-img info imageName &#124; grep 'file format'</code>to check the image format</li></ul></td></tr>
<tr><td>Image Size</td><td><ul><li>Actual image size does not exceed 50 GB, use<code>qemu-img info imageName | grep 'disk size'</code> to check the actual image size</li><li>Image vsize does not exceed 500 GB, use<code>qemu-img info imageName | grep 'virtual size'</code> to check the image vsize</li></ul><b>Note: </b>size information of the image that is converted into QCOW2 format will be used for check upon import</td></tr>
<tr><td>Network</td><td><ul><li>Tencent Cloud provides the <code>eth0</code> network interface for the instance by default</li><li>Tencent Cloud currently does not support IPV6</li><li>Users can query the network configuration of the instance via metadata service. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/4934">Instance Metadata</a></li></ul></td></tr>
<tr><td>Drive</td><td><ul><li>Image must have virtio driver of the virtualization platform KVM installed. For more information, please see<a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux System Check virtio Driver</a></li><li>We recommend you install cloudinit for the image. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/12587">Install Cloud-Init on Linux</a></li><li>If you can not install the cloudinit, please see<a href="https://intl.cloud.tencent.com/document/product/213/12849">Forcibly Import Image</a> to configure the instance</li></ul></td></tr>
<tr><td>Kernel</td><td>Native kernel is preferred for an image. Any modifications may cause failure in importing the image into the CVM</td></tr>
</table>
- **Requirements for Windows images:**
<table>
<tr><th>Image Attribute</th><th>Condition</th></tr>
<tr><td>Operating System</td><td><ul><li>Windows Server 2008, Windows Server 2012, and Windows Server 2016 related versions</li><li>Both 32-bit and 64-bit are supported</li></ul></td></tr>
<tr><td>Image Format</td><td><ul><li>RAW, VHD, QCOW2 and VMDK are supported</li><li>Use<code>qemu-img info imageName &#124; grep 'file format'</code>to check the image format</li></ul></td></tr>
<tr><td>File System Type</td><td><ul><li>Only NTFS that uses MBR partition is supported</li><li>GPT partition is not supported</li><li>Logical Volume Manager (LVM) is not supported</li></ul></td></tr>
<tr><td>Image Size</td><td><ul><li>Actual image size does not exceed 50 GB, use<code>qemu-img info imageName &#124; grep 'disk size'</code> to check the actual image size</li><li>Image vsize does not exceed 500 GB, use<code>qemu-img info imageName &#124; grep 'virtual size'</code> to check the image vsize</li></ul><b>Note: </b>size information of the image that is converted into QCOW2 format will be used for check upon import</td></tr>
<tr><td>Network</td><td><ul><li>Tencent Cloud provides the instance with<code>local connection</code>network interface by default</li><li>Tencent Cloud currently does not support IPV6</li><li>Users can query the network configuration of the instance via metadata service. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/4934">Instance Metadata</a></li></ul></td></tr>
<tr><td>Drive</td><td>Image must have Virtio driver of the virtualization platform KVM installed. Virtio driver is not installed in Windows system by default. Users can install <a href="http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe">Windows Virtio Drive</a> and then export the local image</td></tr>
<tr><td>Others</td><td>Imported Windows system image<b>does not provide </b> <a href="https://intl.cloud.tencent.com/document/product/213/2757">Windows activation</a>service</td></tr>
</table>

## Steps to import images

 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[Images](https://console.cloud.tencent.com/cvm/image)**.
 3. Select **Custom Image** and click **Import Image**.
 4. Following the instructions on the interface, you need to [**enable Cloud Object Storage**](https://console.cloud.tencent.com/cos4/index), [**create bucket**](/doc/product/436/6232), then upload the image file to the bucket and [get Image file URL](/doc/product/436/6260).
 5. Click **Next**.
 6. Fill in the form according to the actual situation, and click **Import**.
 > Be sure to enter the correct COS file URL.
 >
You will be notified whether the import is successful via [Internal Message](https://console.cloud.tencent.com/message).

## Import has failed

The operation to import images on the console may fail due to some reasons. If the import fails, troubleshoot as follows:

### Notes

Before troubleshooting, make sure you have subscribed to product service notifications in the message subscription management page of [Message Center](https://console.cloud.tencent.com/messageCenter/messageConfig). This ensures you can receive internal messages, SMS, and emails about the causes of the failure.
> If you do not subscribe to product service notifications, you will not be able to receive messages about whether the import is successful.

### Troubleshooting the causes of failure

For more information on error messages and descriptions, see [Error Code](# errorcode).

#### InvalidUrl: COS URL is invalid

The InvalidUrl error indicates that a wrong COS URL is entered on the import page. The possible reasons are as follows:
* The image URL you have entered is not a [Tencent Cloud Object Storage](https://console.cloud.tencent.com/cos4/index) image URL.
* Access permission of the COS file is private-read, but the signature has expired.
> COS file URL with the signature can only be accessed once.
>
* COS URL of another region has been entered.
> The image import service accesses COS server in the local region through the private internet.
>
* The user’s image file has been deleted.
After you receive the error message that the COS URL is invalid, troubleshoot based on the reasons above.

#### InvalidFormatSize: format or size does not meet the requirements

The InvalidFormatSize error indicates that the format or size of the image to be imported does not meet the following requirements of Tencent Cloud's image import feature:
* supported image file formats are `qcow2`,` vhd`, `vmdk`, and` raw`.
* The actual file size of the imported image cannot exceed 50 GB (based on the image file converted into qcow2 format).
* The size of the system disk to which the image is imported cannot exceed 500 GB.

After you receive an error message that the format or size does not meet the requirements:
- Covert the image file into an appropriate format according to [Linux Image Creation](https://intl.cloud.tencent.com/document/product/213/17814), reduce the image content to meet the size requirements and then reimport it.
- You can also use the [offline instance migration](https://console.cloud.tencent.com/csm/importOfflineCvm) feature to migrate the instance. This feature supports migration of image files up to 500GB.

#### VirtioNotInstall: Virtio driver is not installed

The VirtioNotInstall error indicates that the image to be imported does not have Virtio driver installed. Tencent Cloud uses KVM virtualization technology and requires users to install Virtio driver on the image to be imported. Except for few customized ones, most Linux operating systems have Virtio driver installed. Windows operating systems require users to manually install Virtio driver:
- For Linux image import, see [Linux System Check virtio Driver](https://intl.cloud.tencent.com/document/product/213/9929).
- For Windows image import, see [Windows Image Creation](https://intl.cloud.tencent.com/document/product/213/17815) to install Virtio driver.

#### CloudInitNotInstalled: cloud-init program is not installed

The CloudInitNotInstalled error indicates that the image to be imported does not have cloud-init program installed. Tencent Cloud uses the open-source cloud-init to initialize the CVM. Therefore, failure to install the cloud-init program will cause the CVM to fail to initialize.
* For Linux image import, see [Install Cloud-Init on Linux](https://intl.cloud.tencent.com/document/product/213/12587).
* For Windows image import, see [Install Cloudbase-Init on Windows](https://intl.cloud.tencent.com/document/product/213/32364).
* After you have installed cloud-init/cloudbase-init, please replace the configuration file according to the document so the CVM can pull data from the correct data source at startup.

#### PartitionNotPresent: Partition information loss

The PartitionNotPresent error indicates that the imported image is incomplete. Please check if the boot partition was included when the image was created.

#### RootPartitionNotFound: Root partition loss

The RootPartitionNotFound error indicates that root partition is not detected in the imported image. Please check the image file and refer to the following possible reasons:
* Installation package file is uploaded.
* Data disk image is uploaded.
* Boot partition image is uploaded.
* Wrong file is uploaded.

#### InternalError: Unknown error

The InternalError error indicates that the image import service does not record the cause of the error. Please contact customer service and our technical personnel will help you resolve the issue as soon as possible.

<a id="errorcode"></a>
## Error Codes
 
| Error Code | Reason | Recommended Processing Method |
|-----|-----|-----|
|InvalidUrl|COS link is invalid|Check if the COS URL is the same as the imported image URL |
| InvalidFormatSize | The format or size does not meet the requirements | The image needs to meet `image format` and `image size` requirements in [Prepare to import](#PreparationsforImport) |
|VirtioNotInstall|The virtio driver is not installed|Install the virtio driver in the image by referring to `Driver' section in [Prepare to import](#PreparationsforImport) |
|PartitionNotPresent|The partition information is not found|The image is corrupted possibly due to incorrect image creation method |
|CloudInitNotInstalled|cloud-init is not installed|Install cloud-init in the Linux image by referring to `Driver' section in [Prepare to import](#PreparationsforImport) |
|RootPartitionNotFound|The root partition is not found|The image is corrupted possibly due to incorrect image creation method |
|InternalError|Other errors|Contact customer service |

