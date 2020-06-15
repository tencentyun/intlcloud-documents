In addition to [creating custom images](https://intl.cloud.tencent.com/document/product/213/4942), Tencent Cloud also allows you to import images. You can import an image file in the system disk of the local server or a server on another platform into CVM custom images. After an image is imported, you can use it to create a CVM or reinstall the operating system (OS) for an existing CVM.

<span id="preparations for import"></span>
## Import Preparations

Prepare an image file that meets import requirements in advance.
- **Requirements for Linux images:**
<table>
<tr><th>Image Attribute</th><th>Requirements</th></tr>
<tr><td>OS</td><td><ul><li>CentOS, Ubuntu, Debian, CoreOS, OpenSUSE, and SUSE</li><li>Both 32-bit and 64-bit OSs are supported.</li></ul></td></tr>
<tr><td>Image format</td><td><ul><li>RAW, VHD, QCOW2, and VMDK</li><li>Run <code>qemu-img info imageName | grep 'file format'</code> to check the image format.</li></ul></td></tr>
<tr><td>File system</td><td>GPT partition is not supported</td></tr>
<tr><td>Image size</td><td><ul><li>The actual image size cannot exceed 50 GB. Run <code>qemu-img info imageName | grep 'disk size'</code> to check the actual image size.</li><li>The image vsize cannot exceed 500 GB. Run <code>qemu-img info imageName | grep 'virtual size'</code> to check the image vsize.</li></ul><b>Note: </b>when an image is imported, the size of the image in QCOW2 format prevails.</td></tr>
<tr><td>Network</td><td><ul><li>Tencent Cloud provides the <code>eth0</code> network interface for the instance by default.</li><li>You can use the metadata service in the instance to check the network configuration of the instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4934">Instance Metadata</a>.</li></ul></td></tr>
<tr><td>Driver</td><td><ul><li>The Virtio driver of the visualization platform KVM must be installed for the image. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking the Virtio Driver on Linux</a>.</li><li>We recommend that you install cloud-init for the image. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/12587">Installing cloud-init on Linux</a>.</li><li>If cloud-init cannot be installed for the image due to other reasons, configure the instance by referring to <a href="https://intl.cloud.tencent.com/document/product/213/12849">Forcibly Importing an Image</a>.</li></ul></td></tr>
<tr><td>Kernel</td><td>The native kernel is preferred for an image. Any modifications on the kernel may cause a failure in importing the image into the CVM.</td></tr>
</table>
- **Requirements for Windows images:**
<table>
<tr><th>Image Attribute</th><th>Requirements</th></tr>
<tr><td>OS</td><td><ul><li>Windows Server 2008, Windows Server 2012, and Windows Server 2016 related versions</li><li>Both 32-bit and 64-bit OSs are supported.</li></ul></td></tr>
<tr><td>Image format</td><td><ul><li>RAW, VHD, QCOW2, and VMDK</li><li>Run <code>qemu-img info imageName | grep 'file format'</code> to check the image format.</li></ul></td></tr>
<tr><td>File system type</td><td><ul><li>Only NTFS with MBR partitions is supported.</li><li>GPT partitions are not supported.</li><li>Logical Volume Manager (LVM) is not supported.</li></ul></td></tr>
<tr><td>Image size</td><td><ul><li>The actual image size cannot exceed 50 GB. Run <code>qemu-img info imageName | grep 'disk size'</code> to check the actual image size.</li><li>The image vsize cannot exceed 500 GB. Run <code>qemu-img info imageName | grep 'virtual size'</code> to check the image vsize.</li></ul><b>Note: </b>when an image is imported, the size of the image in qcow2 format prevails.</td></tr>
<tr><td>Network</td><td><ul><li>Tencent Cloud provides the <code>Local Area Connection</code> network interface for the instance by default. </li><li>You can use the metadata service in the instance to check the network configuration of the instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4934">Instance Metadata</a>.</li></ul></td></tr>
<tr><td>Driver</td><td>The Virtio driver of the visualization platform KVM must be installed for the image. The Virtio driver is not installed in the Windows OS by default. You can install the <a href="http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe">Virtio driver for Windows</a> and then export the local image.</td></tr>
<tr><td>Others</td><td>Imported Windows images <b>do not provide the </b><a href="https://intl.cloud.tencent.com/document/product/213/2757">Windows license activation</a> service.</td></tr>
</table>

## Directions

 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[Images](https://console.cloud.tencent.com/cvm/image)**.
 3. Select **Custom Image** and click **Import Image**.
 4. [Enable Cloud Object Storage](https://console.cloud.tencent.com/cos4/index), and then [create a bucket](/doc/product/436/6232). Upload the image file to the bucket and [obtain the image file URL](/doc/product/436/6260).
 5. Click **Next**.
 6. Complete the form based on the actual situation and click **Import**.
 > Ensure that the entered COS file URL is correct.
 >
You will be notified whether the import is successful through [internal messages](https://console.cloud.tencent.com/message).

## Failed Import

Images may fail to be imported in the console. If the import fails, troubleshoot as follows:

### Notes

Before troubleshooting, ensure that you have subscribed to product service notifications on the [message subscription](https://console.cloud.tencent.com/messageCenter/messageConfig) page. This ensures that you can receive internal messages, SMS messages, and emails about the causes of the failure.
> If you do not subscribe to product service notifications, you will not receive messages about the import result.

### Troubleshooting

For more information on error messages and descriptions, see [Error Codes](# errorcode).

#### InvalidUrl: invalid COS URL

The InvalidUrl error indicates that an incorrect COS URL is entered on the import page. The possible causes include:
* The image URL that you entered is not a [Tencent Cloud Object Storage](https://console.cloud.tencent.com/cos4/index) image URL.
* The access permission of the COS file is private read, and the signature has expired.
> A COS file URL with the signature can be accessed only once.
>
* A COS URL of another region has been entered.
> The image import service accesses the COS server in the local region through a VPC instance.
>
* The user's image file has been deleted.
After you receive the error message stating that the COS URL is invalid, troubleshoot based on the preceding causes.

#### InvalidFormatSize: invalid format or size

The InvalidFormatSize error indicates that the format or size of the image to be imported does not meet the following requirements of the Tencent Cloud's image import feature:
* Supported image file formats are `qcow2`,` vhd`, `vmdk`, and` raw`.
* The actual image file size cannot exceed 50 GB (based on the converted image file in qcow2 format).
* The size of the system disk to which the image is imported cannot exceed 500 GB.

After you receive an error message stating that the format or size is invalid:
- Convert the image file into an appropriate format according to [Linux Image Creation](https://intl.cloud.tencent.com/document/product/213/17814), reduce the image size to meet the size requirements, and then reimport it.
- You can also use the [offline instance migration](https://console.cloud.tencent.com/csm/importOfflineCvm) feature to migrate the instance. This feature supports the migration of an image file with a size up to 500 GB.

#### VirtioNotInstall: the Virtio driver is not installed

The VirtioNotInstall error indicates that the image to be imported does not have the Virtio driver installed. Tencent Cloud uses the KVM virtualization technology and requires users to install the Virtio driver on the image to be imported. Except for a few customized Linux OSs, most Linux OSs have the Virtio driver installed. In Windows OSs, users need to manually install the Virtio driver:
- For Linux image import, see [Checking the Virtio Driver on Linux](https://intl.cloud.tencent.com/document/product/213/9929).
- For Windows image import, see [Windows Image Creation](https://intl.cloud.tencent.com/document/product/213/17815) to install the Virtio driver.

#### CloudInitNotInstalled: the cloud-init program is not installed

The CloudInitNotInstalled error indicates that the image to be imported does not have the cloud-init program installed. Tencent Cloud uses the open-source cloud-init program to initialize the CVM. If the cloud-init program is not installed, the CVM will fail to be initialized.
* For Linux image import, see [Installing cloud-init on Linux](https://intl.cloud.tencent.com/document/product/213/12587).
* For Windows image import, see [Installing cloudbase-init on Windows](https://intl.cloud.tencent.com/document/product/213/32364).
* After you install cloud-init or cloudbase-init, replace the configuration file according to the related document so that the CVM can pull data from the correct data source upon startup.

#### PartitionNotPresent: partition information is lost

The PartitionNotPresent error indicates that the imported image is incomplete. In this case, check whether the boot partition was included when the image was created.

#### RootPartitionNotFound: the root partition is lost

The RootPartitionNotFound error indicates that the root partition cannot be detected in the image to be imported. In this case, check the image file. The possible causes include:
* The installation package is uploaded.
* The data disk image is uploaded.
* The boot partition image is uploaded.
* An incorrect file is uploaded.

#### InternalError: unknown error

The InternalError error indicates that the image import service does not record the cause of the error. In this case, contact our customer service. Our technical personnel will help you resolve the issue as soon as possible.

<a id="errorcode"></a>
## Error Codes
 
| Error Code | Reason | Recommended Solution |
|-----|-----|-----|
| InvalidUrl | The COS link is invalid. | Check whether the COS URL is the same as the imported image URL. |
| InvalidFormatSize | The format or size does not meet requirements. | Images need to meet the `image format` and `image size` requirements described in [Import Preparations](#PreparationsforImport). |
| VirtioNotInstall | The Virtio driver is not installed. | Install the Virtio driver in the image by referring to the `Driver` section in [Import Preparations](#PreparationsforImport). |
| PartitionNotPresent | Partition information is not found. | The image is corrupted possibly due to an incorrect image creation method. |
| CloudInitNotInstalled | The cloud-init program is not installed. | Install cloud-init in the Linux image by referring to the `Driver` section in [Import Preparations](#PreparationsforImport). |
| RootPartitionNotFound | The root partition is not found. | The image is corrupted possibly due to an incorrect image creation method. |
| InternalError | An internal error other than the preceding ones occurs. | Contact our customer service. |

