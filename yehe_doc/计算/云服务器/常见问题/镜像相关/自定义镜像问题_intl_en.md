### What should I do if the Windows system fails to create a custom image?

If the Windows system fails to create a custom image, you can troubleshoot the issue as follows:
1. The creation of a custom image relies on the Windows Modules Installer provided by Microsoft. Make sure this service is working properly.
2. Some antivirus tools or Safedog may block custom image creation scripts from being executed. To avoid creation failure, we recommend you disable these tools before creating a custom image.
3. If the image creation tool is interrupted by system pop-ups, remotely log in to the CVM and check and adjust the CVM configuration to block pop-ups.

### Can a custom image be created from the data disk snapshot?
No. A custom image can be created from the system disk snapshot, but not from the data disk snapshot.
If you need to keep the data on the data disk of the original instance when launching a new instance, you can first take a snapshot of the data disk, and then use this data disk snapshot to create a new CBS data disk. For more information, see [Creating Cloud Disks using Snapshots](https://www.tencentcloud.com/document/product/362/5757).

### Do local disks support custom images?
- If the system disk of an instance is a local disk, you can create custom images.
- If the data disk of an instance is a local disk, you can create only images of the system disk of the instance.

### How do I confirm that a data disk has been unmounted and a custom image can be created?
1. Confirm that the partition statement row of the automatically mounted data disk has been deleted in the `/etc/fstab` file.
2. Execute the `mount` command to query the mounting information of all devices. Ensure that the execution result does not include the corresponding data disk partition information.

### Will the custom image still exist after the instance is released?
Yes.

### Can I change the operating system of an instance created from a custom image? After I change the operating system, will I still be able to use the original custom image?
Yes. You can continue to use the original custom image after changing the operating system.


### Can I upgrade the CPU, memory, bandwidth, disk, and other configurations of a CVM instance enabled by a custom image?
Yes. You can upgrade all of them. For more information, see [Change Instance Configuration](https://www.tencentcloud.com/document/product/213/2178) and [Adjust Network Configuration](https://www.tencentcloud.com/document/product/213/15517).

### Can a custom image be used across regions?
No. A custom image can only be used in the same region. For example, you cannot directly launch a CVM instance in East China (Nanjing) using the custom image created from a CVM instance in East China (Shanghai).
To use a custom image across regions, copy the image to the target region first. For more information, see [Copying Images](https://www.tencentcloud.com/document/product/213/4943).

### Where can I view the image creation progress? How long does it take to create an image?
You can view the image creation progress on the **Images** page of the CVM Console. The time it takes to create an image depends on the size of the instance’s data.

