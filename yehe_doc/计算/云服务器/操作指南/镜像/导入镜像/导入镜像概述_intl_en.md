In addition to the feature of [creating custom images](https://intl.cloud.tencent.com/document/product/213/4942), Tencent Cloud also supports importing images. You can import an image file of a server system disk on the local computer or another platform into a Cloud Virtual Machine (CVM) custom image. After the image is imported, you can use it to create a CVM instance or reinstall the system for the existing CVM instance.

<span id="import preparations"></span>
## Preparations

Prepare an image file that meets the import requirements.
- **Requirements for Linux images:**
<table>
<tr><th>Image Attribute</th><th>Requirement</th></tr>
<tr><td>Operating system</td><td><ul><li>CentOS, Ubuntu, Debian, CoreOS, openSUSE, and SUSE</li><li>32-bit or 64-bit</li></ul></td></tr>
<tr><td>Image format</td><td><ul><li>RAW, VHD, QCOW2, or VMDK</li><li>You can run <code>qemu-img info imageName &#124; grep 'file format'</code> to check the image format.</li></ul></td></tr>
<tr><td>Image size</td><td><ul><li>The actual image size cannot exceed 50 GB. You can run <code>qemu-img info imageName &#124; grep 'disk size'</code> to check the actual image size.</li><li>The image vsize cannot exceed 500 GB. You can run <code>qemu-img info imageName &#124; grep 'virtual size'</code> to check the image vsize.</li></ul><b>Note: </b>The image size checked upon the import of an image is subject to the size obtained after the image is converted to the QCOW2 format.</td></tr>
<tr><td>Network</td><td><ul><li>Tencent Cloud provides the <code>eth0</code> network interface for the instance by default.</li><li>You can use the metadata service in the instance to check the network configuration of the instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4934">Metadata of the Instance</a></li></ul></td></tr>.
<tr><td>Driver</td><td><ul><li>The virtIO driver of the visualization platform KVM must be installed for the image. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking the virtIO Driver in the Linux System</a>.</li><li>It is recommended that you install cloud-init for the image. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/12587">Installing cloud-init Before Importing a Linux Image</a>.</li><li>If cloud-init cannot be installed for the image due to other reasons, manually configure the instance by referring to <a href="https://intl.cloud.tencent.com/document/product/213/12849">Forcibly Importing an Image</a>.</li></ul></td></tr>
<tr><td>Kernel</td><td>A native kernel is preferred for an image. Any modification of the kernel may cause the failure in importing the image into the CVM instance.</td></tr>
</table>
- **Requirements for Windows images:**
<table>
<tr><th>Image Attribute</th><th>Requirement</th></tr>
<tr><td>Operating system</td><td><ul><li>Windows Server 2012 or Windows Server 2016</li><li>32-bit or 64-bit</li></ul></td></tr>
<tr><td>Image format</td><td><ul><li>RAW, VHD, QCOW2, or VMDK</li><li>You can run <code>qemu-img info imageName &#124; grep 'file format'</code> to check the image format.</li></ul></td></tr>
<tr><td>File system type</td><td><ul><li>Only the NTFS file system that uses MBR partitioning is supported.</li><li>GPT partitioning is not supported.</li><li>Logical Volume Management (LVM) is not supported.</li></ul></td></tr>
<tr><td>Image size</td><td><ul><li>The actual image size cannot exceed 50 GB. You can run <code>qemu-img info imageName &#124; grep 'disk size'</code> to check the actual image size.</li><li>The image vsize cannot exceed 500 GB. You can run <code>qemu-img info imageName &#124; grep 'virtual size'</code> to check the image vsize.</li></ul><b>Note: </b>The image size checked upon the import of an image is subject to the size obtained after the image is converted to the QCOW2 format.</td></tr>
<tr><td>Network</td><td><ul><li>Tencent Cloud provides the <code>Local Area Connection</code> network interface for the instance by default. </li><li>You can use the metadata service in the instance to check the network configuration of the instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4934">Metadata of the Instance</a>.</li></ul></td></tr>
<tr><td>Driver</td><td>The virtIO driver of the visualization platform KVM must be installed for the image. The virtIO driver is not installed by default in the Windows system. You can install the <a href="http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe">Windows virtIO driver</a> before importing a local image.</td></tr>
<tr><td>Others</td><td>The imported Windows image <b>does not provide</b> the <a href="https://intl.cloud.tencent.com/document/product/213/2757">Windows activation</a> service.</td></tr>
</table>

## Import Directions

 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[Image](https://console.cloud.tencent.com/cvm/image)**.
 3. Click **Custom Image** and then **Import Image**.
 4. [Enable Cloud Object Storage (COS)](https://console.cloud.tencent.com/cos4/index), [create a bucket](/doc/product/436/6232), upload the image file to the bucket, and [obtain the image file URL](/doc/product/436/6260).
 5. Click **Next**.
 6. Complete the form according to the actual situation and click **Import**.
 > Ensure that the entered COS file URL is correct.
 >
An [internal message](https://console.cloud.tencent.com/message) will be sent to inform you of the import result.

## Import Failures

The attempt to import an image in the console may fail for several reasons. If the import task fails, troubleshoot the fault as follows.

### Notes

Before troubleshooting, subscribe to the product-related notifications in the message subscription column of [Message Center](https://console.cloud.tencent.com/messageCenter/messageConfig) so that you can receive internal messages, SMS messages, and emails that contain the reasons for failure.
> If you do not subscribe to the product-related notifications in the message center, you cannot receive any internal messages that indicate the import result (success or failure).

### Troubleshooting

For more information on detailed error messages and descriptions, see [Error Codes](#errorcode).

#### InvalidUrl: invalid COS URL

The InvalidUrl error indicates that an incorrect COS URL was entered on the **Import Image** page. The possible reasons are:
* The entered image URL is not a URL of [Cloud Object Storage](https://console.cloud.tencent.com/cos4/index).
* The access permission of the COS file is private-read, but the signature is expired.
> The URL of the COS file with the signature can be accessed only once.
>
* The COS URL of another region was entered.
> The image import service accesses the COS server in the local region through the private network.
>
* The user's image file has been deleted.
When you get the InvalidUrl error, troubleshoot the fault according to the preceding reasons.

#### InvalidFormatSize: invalid format or size

The InvalidFormatSize error indicates that the format or size of the image to be imported does not meet the following requirements of the image import feature:
* The following image file formats are supported: `qcow2`, `vhd`, `vmdk`, and `raw`.
* The actual image size cannot exceed 50 GB. The actual image size refers to the size obtained after the image is converted to the QCOW2 format.
* The size of the system disk to which the image is imported cannot exceed 500 GB.

When you get the InvalidFormatSize error, resolve the fault as follows:
- Based on the image format conversion method described in [Preparing a Linux Image](https://intl.cloud.tencent.com/document/product/213/17814), convert the image file into an appropriate file format and ensure that its format and size meet the requirements. Then, import the image again.
- Use the [offline instance migration](https://console.cloud.tencent.com/csm/importOfflineCvm) feature to migrate the instance. This feature supports the migration of an image file with a size up to 500 GB.

#### VirtioNotInstall: virtIO driver not installed

The VirtioNotInstall error indicates that the virtIO driver is not installed. Tencent Cloud uses the KVM visualization technology, which requires that the virtIO driver be installed in the imported image. In most Linux operating systems except for some custom ones, the virtIO driver is already installed. In the Windows operating system, however, users must manually install the virtIO driver.
* To import a Linux image, install the virtIO driver by referring to [Checking the virtIO Driver in the Linux System](https://intl.cloud.tencent.com/document/product/213/9929).
- To import a Windows image, install the virtIO driver by referring to [Preparing a Windows Image](https://intl.cloud.tencent.com/document/product/213/17815).

#### CloudInitNotInstalled: cloud-init is not installed

The CloudInitNotInstalled error indicates that the cloud-init program is not installed. Tencent Cloud uses the open-source cloud-init program. Therefore, if cloud-init is not installed, the initialization of the user's CVM instance fails.
* To import a Linux image, install cloud-init by referring to [Installing cloud-init in the Linux System](https://intl.cloud.tencent.com/document/product/213/12587).
* To import a Windows image, install cloud-init by referring to [Installing cloudbase-init in the Windows System](https://intl.cloud.tencent.com/document/product/213/32364).
* After installing cloud-init or cloudbase-init, replace the configuration file so that the CVM instance pulls data from the correct data source upon launch.

#### PartitionNotPresent: partition information was lost

The PartitionNotPresent error indicates that the imported image is incomplete. In this case, check whether the image contains the boot partition when preparing the image.

#### RootPartitionNotFound: root partition was lost

The RootPartitionNotFound error indicates that the root partition cannot be detected in the imported image. In this case, ycheck the image file. The following possible reasons for this error are provided for your reference:
* The installation package is uploaded.
* The data disk image is uploaded.
* The boot partition image is uploaded.
* The uploaded file is incorrect.

#### InternalError: unknown error

The InternalError error indicates that the cause of the error is not recorded in the image import service yet. In this case, contact customer service, and our technical personnel will help you solve the problem as soon as possible.

<a id="errorcode"></a>
## Error Codes
 
| Error Code | Reason | Recommended Solution |
|-----|-----|-----|
| InvalidUrl | The COS URL is invalid. | Check whether the COS URL is the same as the image import URL. |
| InvalidFormatSize | The format or size does not meet the requirements. | The image must meet the requirements for the `image format` and `image size` described in [Preparations](#Import Preparations). |
| VirtioNotInstall | The virtIO driver is not installed. | Install the virtIO driver in the image by referring to the `Driver` section in [Preparations](#Import Preparations). |
| PartitionNotPresent | Partition information cannot be found. | The image is corrupted possibly because of the improper image preparation method. |
| CloudInitNotInstalled | cloud-init is not installed. | Install cloud-init for the Linux image by referring to the `Driver` section in [Preparations](#Import Preparations). |
| RootPartitionNotFound | The root partition cannot be detected. | The image is corrupted possibly because of the improper image preparation method. |
| InternalError | Other errors. | Contact customer service. |

