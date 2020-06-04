### What should I do if the Windows system fails to create a custom image?

If the Windows system fails to create a custom image, check by following the steps below:
1. The creation of a custom image relies on the Windows Modules Installer provided by Microsoft. Make sure this service is working properly.
2. Some antivirus tools or Safedog may block custom image creation scripts from executing. To avoid creation failure, we recommend you close these tools before creating a custom image.
3. If the image creation tool is interrupted by system pop-ups, remotely log in to the CVM, and then check and adjust the CVM configuration to avoid pop-ups.

### Can a custom image be created from the data disk snapshot?
The custom image can be created from a snapshot of the system disk, but not the data disk.
If you need to keep the data on the data disk of the original instance when starting a new instance, you can first take a snapshot of the data disk, and then use this data disk snapshot to create a new CBS data disk. For more information, see [Creating Cloud Disks using Snapshots](https://intl.cloud.tencent.com/document/product/362/5757).

### How do I confirm the data disk has been unmounted and a custom image can be created?
1. Confirm the partition statement line of the data disk that has been automatically mounted is deleted in the `/etc/fstab` file.
2. Execute the `mount` command to query the mounting information of all devices, and ensure no data disk partition exists in the execution result.

### Does the custom image still exist after the instance is released?
Yes.

### Can I change the operating system of an instance created from custom images? Is the original custom image usable after I change the operating system?
Yes, you can continue to use the original custom image after changing the operating system.


### Can I upgrade CPU, memory, bandwidth, disk and other configurations of a CVM instance launched from a custom image?
Yes, you can upgrade all of them. For more information, see [Changing Instance Configuration](https://intl.cloud.tencent.com/document/product/213/2178) and [Adjusting Network Configuration](https://intl.cloud.tencent.com/document/product/213/15517).

### Can a custom image be used cross regions?
No. The custom image can only be used in the same region. For example, you cannot directly launch a CVM instance in East China (Nanjing) using the custom image created from a CVM instance in East China (Shanghai).
To use a custom image cross regions, first copy the image to the target region. For more information, see [Copying Images](https://intl.cloud.tencent.com/document/product/213/4943).

### Where can I view the image creation progress? How long it takes?
You can view the progress on the **Images** page of the CVM console. The time depends on the data size of the instance.


