## Overview

This document describes how to prepare a Windows image by using the Windows Server 2012 operating system as an example.

## Directions

### Preparations

Before preparing and exporting a system disk image, complete the following checks.
>? If you need to prepare and export a data disk image, skip this step.
>
#### Check the partitioning mode and startup mode of the OS

1. On the desktop, click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> to open the **Windows PowerShell** window.
2. In the **Windows PowerShell** window, enter **diskmgmt.msc** and press **Enter**. The **Disk Management** window appears.
3. Right-click the disk to be checked, choose **Properties**, select the **Volume** tab, and check the disk partitioning mode.
4. Check whether the disk partitioning mode is GPT.
 - If yes, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) because service migration currently does not support the GPT partition.
 - If no, proceed with the next step.
5. Start CMD as admin and run the following command to check whether the operating system starts in EFI mode:
```
bcdedit /enum {current}
```
A result similar to the following will be returned:
```
Windows boot loader
ID                  {current}
device                  partition=C:
path                    \WINDOWS\system32\winload.exe
description             Windows 10
locale                  zh-CN
inherit                 {bootloadersettings}
recoverysequence        {f9dbeba1-1935-11e8-88dd-ff37cca2625c}
displaymessageoverride  Recovery
recoveryenabled         Yes
flightsigning           Yes
allowedinmemorysettings 0x15000075
osdevice                partition=C:
systemroot              \WINDOWS
resumeobject            {1bcd0c6f-1935-11e8-8d3e-3464a915af28}
nx                      OptIn
bootmenupolicy          Standard
```
 - If `path` contains "efi", the operating system starts in EFI mode. In this case, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).
 - If `path` does not contain "efi", proceed with the next step.

#### Unmounting software

Unmount the conflicting drivers and software programs (including VMware tools, Xen tools, Virtualbox GuestAdditions, and other software that comes with underlying drivers).

#### Installing cloud-base

Install cloud-base as instructed in [Installing Cloudbase-Init on Windows](https://intl.cloud.tencent.com/document/product/213/32364).

#### Checking or installing the virtIO driver

1. Choose **Control Panel** > **Programs and Features**, and enter "Virtio" in the search box.
 - If the result as shown in the following figure is returned, the Virtio driver has been installed.
![image](https://main.qcloudimg.com/raw/87808940ddd5317dd8c67a699e3dc5c0.png
)
 - If no Virtio driver is installed, please manually install one.
    - For Microsoft Windows Server 2008 R2 (Standard Edition, DataCenter Edition, and Enterprise Edition), and Microsoft Windows Server 2012 R2 (Standard Edition), download Virtio for Tencent Cloud at:
      - Public network download address: `http://mirrors.tencent.com/install/windows/virtio_64_10003.msi`
      - Private network download address: `http://mirrors.tencentyun.com/install/windows/virtio_64_10003.msi`
    - For other system versions, download [Virtio for Community Edition](https://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers).

#### Checking other hardware configurations

After the migration to the cloud, hardware changes include but are not limited to:
 - The graphics card is changed to Cirrus VGA.
 - The disk is changed to Virtio Disk.
 - The NIC is changed to Virtio Nic, and Local Area Connection is used by default.

### Exporting an image

You can use a variety of tools to export an image as needed.
- [Using a platform tool to export an image](#Useplatform)
- [Using Disk2vhd to export an image](#Usedisk2vhd).

<span id="Useplatform"></span>
#### Using a platform tool to export an image

For more information on how to use the image export tools of virtualization platforms, such as VMWare vCenter Convert and Citrix XenConvert, see the document for the respective platform.
>? Tencent Cloud Service Migration supports images in qcow2, vhd, raw, and vmdk formats.
>

<span id="Usedisk2vhd"></span>
#### Using Disk2vhd to export an image

To export the system on a physical machine or if you do not want to use a platform tool to export an image, use Disk2vhd instead.
1. Install and start the Disk2vhd tool.
[Click here to download Disk2vhd](https://download.sysinternals.com/files/Disk2vhd.zip).
2. Select the storage path of the image to export, select the volumes to copy, and click **Create**, as shown in the following figure.
>! 
> - Disk2vhd can be started only after the Volume Shadow Copy Service (VSS) is installed in the Windows system. For more information about the VSS features, see [Volume Shadow Copy Service](https://docs.microsoft.com/zh-cn/windows/win32/vss/volume-shadow-copy-service-portal?redirectedfrom=MSDN).
> - Do not select "Use Vhdx" because the system currently does not support images in VHDX format.
> - We recommend that you select "Use volume Shadow Copy" to better ensure data integrity.
> 
![image](https://main.qcloudimg.com/raw/68d9c4e5e7db49c4cefdd3785ce9b68d.jpg)

### Checking the image

>? The image file system that you prepare may be corrupted because you prepared the image without stopping the service or due to other reasons. Therefore, we recommend that you check the image after preparing it.
>
If the image format is supported by the current platform, you can directly open the image to check the file system. For example, the Windows platform supports the VHD image, the Linux platform allows you to use qemu-nbd to open QCOW2 images, and the Xen platform allows you to directly open the VHD files.
Take the Linux platform as an example:
```
modprobe nbd
qemu-nbd -c /dev/nbd0 xxxx.qcow2
mount /dev/nbd0p1 /mnt
```
If the file system is corrupted when the first partition of the QCOW2 image is exported, an error occurs when you run the `mount` command.
You can also start the CVM to check whether the image file works before uploading the image.
