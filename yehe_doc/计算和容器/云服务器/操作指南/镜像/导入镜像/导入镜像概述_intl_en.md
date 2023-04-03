In addition to [creating a custom image](https://intl.cloud.tencent.com/document/product/213/4942), Tencent Cloud allows you to import images. You can import an image file of the system disk on a local or a different server into CVM custom images. You can use the imported image to create a CVM or reinstall the operating system for an existing CVM.


## Import Preparation[](id:importPreparation)

Prepare an image file that meets the import requirements.

<dx-tabs>
::: Linux images
<table>
<tr><th style="width:17%">Image Attribute</th><th>Requirements</th></tr>
<tr><td>OS</td><td><ul><li>CentOS、CentOS Stream、Ubuntu、Debian、OpenSUSE、CoreOS、FreeBSD、AlmaLinux、Rocky Linux、Fedora、Kylin、UnionTech、TencentOS</li><li>Both 32-bit and 64-bit OSs are supported</li></ul></td></tr>
<tr><td>Image format</td><td><ul><li>RAW, VHD, QCOW2, and VMDK</li><li>Run <code>qemu-img info imageName | grep 'file format'</code> to check the image format.</li></ul></td></tr>
<tr><td>File system type</td><td>GPT partition is not supported</td></tr>
<tr><td>Image size</td><td><ul><li>The actual image size cannot exceed 50 GB. Run <code>qemu-img info imageName | grep 'disk size'</code> to check the image size.</li><li>The image vsize cannot exceed 500 GB. Run <code>qemu-img info imageName | grep 'virtual size'</code> to check the image vsize.</li></ul><b>Note: </b>size of an image in QCOW2 format is used upon check during import.</td></tr>
<tr><td>Network</td><td><ul><li>By default, Tencent Cloud provides the <code>eth0</code> network interface for the instance.</li><li>You can use the metadata service to query the network configuration of the instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4934">Instance Metadata</a>.</li></ul></td></tr>
<tr><td>Driver</td><td><ul><li>Virtio driver of the virtualization module KVM must be installed for an image. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking Virtio Drivers in Linux</a>.</li><li>We recommend installing cloud-init for the image. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/12587">Installing Cloud-Init on Linux</a>. </li><li>If cloud-init cannot be installed, configure the instance by referring to <a href="https://intl.cloud.tencent.com/document/product/213/12849">Forcibly Import Image</a>.</li></ul></td></tr>
<tr><td>Kernel</td><td>Native kernel is preferred for an image. Any modifications on the kernel may cause the import to fail.</td></tr>
<tr><td>Region</td><td>Importing images from COS in another region is unavailable for the Shanghai Finance and Shenzhen Finance.</td></tr>
</table>

:::
::: Windows images
<table>
<tr><th style="width:16%">Image Attribute</th><th>Requirements</th></tr>
<tr><td>OS</td><td><ul><li>Windows Server 2008, Windows Server 2012, Windows Server 2016 related versions, Windows Server 2019 related versions, and Windows Server 2022 related versions</li><li>Both 32-bit and 64-bit OSs are supported.</li></ul></td></tr>
<tr><td>Image format</td><td><ul><li>RAW, VHD, QCOW2, and VMDK</li><li>Run <code>qemu-img info imageName | grep 'file format'</code> to check the image format.</li></ul></td></tr>
<tr><td>File system type</td><td><ul><li>Only NTFS with MBR partition is supported.</li><li>GPT partition is not supported.</li><li>Logical Volume Manager (LVM) is not supported.</li></ul></td></tr>
<tr><td>Image size</td><td><ul><li>The actual image size cannot exceed 50 GB. Run <code>qemu-img info imageName | grep 'disk size'</code> to check the image size.</li><li>The image vsize cannot exceed 500 GB. Run <code>qemu-img info imageName | grep 'virtual size'</code> to check the image vsize.</li></ul><b>Note: </b>size of an image in QCOW2 format is used upon check during import.</td></tr>
<tr><td>Network</td><td><ul><li>By default, Tencent Cloud provides <code>local area connection</code> network interface for the instance. </li><li>You can use the metadata service to query the network configuration of the instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4934">Instance Metadata</a>.</li></ul></td></tr>
<tr><td>Driver</td><td>Virtio driver of the virtualization module KVM must be installed for an image. The Windows system does not come with a Virtio driver by default, so first install the Windows Virtio driver before exporting a local image. Choose the download address based on the network environment:<ul><li>Public network download address:<code>http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe</code></li><li>Private network download address:<code>http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe</code></li></ul></td></tr>
<tr><td>Region</td><td>Importing images from COS in another region is unavailable for the Shanghai Finance and Shenzhen Finance.</td></tr>
<tr><td>Others</td><td>Imported Windows images <b>do not support </b><a href="https://intl.cloud.tencent.com/document/product/213/2757">Windows system activation</a>.</td></tr>
</table>

:::
</dx-tabs>


## Directions

 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=19) and click [**Images**](https://console.cloud.tencent.com/cvm/image) on the left sidebar.
 2. Select **Custom image** and click **Importing an image**.
 3. As prompted in the operation interface, first [enable COS](https://console.cloud.tencent.com/cos4/index), and then [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309). [Uploading an Object](https://www.tencentcloud.com/document/product/436/13321) the image file to the bucket and [get the image file URL](https://intl.cloud.tencent.com/document/product/436/13322).
 4. Click **Next**.
 5. Complete the configurations and click **Import**.
<dx-alert infotype="notice" title="">
Ensure the entered COS file URL is correct.
</dx-alert>
You will be notified about the result of import via <a href="https://console.cloud.tencent.com/message">Message Center</a>.

## Failed Imports

If the import failed, troubleshoot as follows:

### Notes

Make sure you have subscribed to product service notifications via [Message Subscription](https://console.cloud.tencent.com/messageCenter/messageConfig). This ensures you can receive notifications from Message Center, SMS messages, and emails about the cause of failure.


<dx-alert infotype="notice" title="">
If you do not subscribe to product service notifications, you will not receive the notification from Message Center about whether an import is successful.
</dx-alert>



### Troubleshooting

You can refer to the following information for troubleshooting on errors. See [error code ](#errorcode) for detailed error prompt and error description.


<dx-accordion>
::: InvalidUrl: invalid COS URL
The InvalidUrl error indicates that an incorrect COS URL has been entered. The possible causes are:
* The image URL you entered is not a [Cloud Object Storage](https://console.cloud.tencent.com/cos4/index) image URL.
* The permission of the COS URL is not public read and private write.
* The access permission of the COS file is private read, but the signature has expired.
<dx-alert infotype="notice" title="">
COS URL with the signature can only be accessed once.
</dx-alert>
* When importing an image outside the Chinese mainland, a COS link in a different region is used.
<dx-alert infotype="notice" title="">
The image import service outside the Chinese mainland only supports COS instances in the same region; that is, a COS link in the same region needs to be used for import.
</dx-alert>
* The user's image file has been deleted.
If you receive the error message about an invalid COS URL, troubleshoot based on the reasons above.
:::
::: InvalidFormatSize: invalid format or size
The InvalidFormatSize error indicates that the format or size of an image to be imported does not meet the following requirements of Tencent Cloud:
* Supported image file formats are `qcow2`,`vhd`, `vmdk`, and` raw`.
* The size of an image file to be imported cannot exceed 50 GB (based on the size in qcow2 format).
* The size of the system disk to which the image is imported cannot exceed 500 GB.

If you receive an error message that the image format or size is invalid:
- Convert the image file into an appropriate format according to [Linux Image Creation](https://intl.cloud.tencent.com/document/product/213/17814), reduce the image content to meet the size requirements and then reimport it.
- Or migrate instance through [Offline Instance Migration](https://intl.cloud.tencent.com/document/product/213/19233). This feature supports the migration of up to 500 GB image files.
:::
::: VirtioNotInstall: Virtio driver not installed
The VirtioNotInstall error indicates that the image to be imported does not have Virtio driver installed. Tencent Cloud uses the KVM virtualization technology and requires users to install Virtio driver on the image to be imported. Except for a few customized Linux OSs, most Linux OSs have Virtio driver installed. In Windows OSs, users need to manually install the Virtio driver:
- For Linux image import, see [Checking Virtio Drivers in Linux](https://intl.cloud.tencent.com/document/product/213/9929).
- For Windows image import, see [Preparing a Windows Image](https://intl.cloud.tencent.com/document/product/213/17815) to install the Virtio driver.
:::
::: CloudInitNotInstalled: cloud-init program not installed
The CloudInitNotInstalled error indicates that the image to be imported does not have cloud-init installed. Tencent Cloud uses the open-source cloud-init software to initialize the CVM. If cloud-init is not installed, the CVM initialization will fail.
* For Linux image import, see [Installing Cloud-Init on Linux](https://intl.cloud.tencent.com/document/product/213/12587).
* For Windows image import, see [Installing Cloudbase-Init on Windows](https://intl.cloud.tencent.com/document/product/213/32364).
* After cloud-init or cloudbase-init is installed, replace the configuration file based on the corresponding document so the CVM can pull data from the correct data source upon startup.
:::
::: PartitionNotPresent: partition information not found
The PartitionNotPresent error indicates that the imported image is incomplete. Check whether the boot partition was included when the image was created.
:::
::: RootPartitionNotFound: root partition not found
The RootPartitionNotFound error indicates that the root partition cannot be detected in the image to be imported. Check the image file. The possible causes are:
* The installation package was uploaded.
* The data disk image was uploaded.
* The boot partition image was uploaded.
* An incorrect file was uploaded.
:::
::: InternalError: unknown error
The InternalError error indicates that the cause of error has not yet been recorded. Contact the customer service and our technical personnel will help you resolve the issue.
:::
</dx-accordion>



## Error Code[](id:errorcode)
 
| Error Code | Reason | Recommended Solution |
|-----|-----|-----|
| InvalidUrl | Invalid COS link. | Check whether the COS URL is the same as the imported image URL. |
| InvalidFormatSize | Format or size does not meet requirements. | Images must meet the `image format` and `image size` requirements in [Preparations](https://www.tencentcloud.com/document/product/213/4945). |
| VirtioNotInstall | Virtio driver not installed. | Install the Virtio driver in the image by referring to the `Driver` section in [Preparations](https://www.tencentcloud.com/document/product/213/4945). |
| PartitionNotPresent | Partition information not found. | Image is corrupted possibly due to incorrect image creation method. |
| CloudInitNotInstalled | Cloud-init software not installed. | Install cloud-init in the Linux image by referring to the `Driver` section in [Preparations](https://www.tencentcloud.com/document/product/213/4945). |
| RootPartitionNotFound | Root partition not found. | Image is corrupted possibly due to incorrect image creation method. |
| InternalError | Other errors. | Contact our customer service. |

