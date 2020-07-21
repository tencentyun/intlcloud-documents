## Overview

A device fingerprint is a unique hardware device identifier collected from a physical server. Like human fingerprints, device fingerprints vary by device.

A white-box key can be bound to one or multiple devices by integrating with the corresponding device fingerprints, so that decryption can be performed only on the bound devices, which further enhances and protects the security of sensitive information.

## Directions

1. The admin logs in to the [KMS Console](https://console.cloud.tencent.com/kms2/whitebox) and enters the customer managed CMK management page.
2. Click **Download Device Fingerprint Capture Tool**. In the download dialog box that pops up, select the operating system of the devices to be bound and click **Download** to download the corresponding tool.
![](https://main.qcloudimg.com/raw/3f0046a8b298670a2469d1d174093f8e.jpg)
3. The admin distributes the device fingerprint capture tool to the system OPS engineer and indicates the devices whose fingerprints need to be captured.
4. The system OPS engineer logs in to the operating system of the target devices and run the device fingerprint capture tool to capture the fingerprints as shown below:                   
 ![](https://main.qcloudimg.com/raw/5cffd4eb6bb33454f1dc797cb7d6e1f7.png)
>!The device fingerprint capture tool supports only Windows and Linux and should run on the operating system of the hosts. Currently, only physical servers and Tencent Cloud CVM instances are supported, while Docker environments are not.
5. The system OPS engineer sends the list of captured device fingerprints to the admin.
>?According to the actual use case and permission control policy, the system OPS engineer and the console admin can be the same person.
6. On the customer managed CMK management page in the [KMS Console](https://console.cloud.tencent.com/kms2/whitebox), the admin selects the white-box key to be bound to the fingerprints.
	- If the white-box key is new or hasn't been bound to any device fingerprints, click **Add Device Fingerprint**.
	- If the white-box key has been bound to device fingerprints, click **Manage Device Fingerprint**. ![](https://main.qcloudimg.com/raw/5d0c894e066915cfda5a2dea8e7a466d.jpg)
7. In the pop-up dialog box, enter the captured device fingerprints and their description in either of the following ways:
 - Click **Add Device Fingerprint** and directly enter the information on the page:
		![](https://main.qcloudimg.com/raw/c1d9196dc60ae9c793654ec910e6cd0a.jpg)
 - Click **Download Batch Upload and Import Template**, enter the information in the downloaded CSV file, and save it. Click **Batch Upload** and select the saved CSV file to upload the fingerprint information in batches.
Sample CSV file content:
```plaintext
Device fingerprint,description
123456,test description
```
8. After the fingerprints are entered, click **OK** to bind the white-box key to the list of specified device fingerprints.
9. After the device fingerprints are bound, error 01000016 will occur if decryption is performed on an unbound device as shown below:
![](https://main.qcloudimg.com/raw/1daffff932bf43647301a32066a8785c.png) 



## Notes

1. Device binding is an enhancement on the white-box key feature, which is optional.
 - If no devices are bound, decryption with the white-box key can be performed on any device.
 - If devices are bound, decryption with the white-box key can be performed only on the bound devices.
2. **Device fingerprint binding should be performed before decryption key download;** otherwise, the binding will not take effect.
3. The device fingerprint capture tool supports only Windows and Linux and should run on the operating system of the hosts. Currently, only physical servers and Tencent Cloud CVM instances are supported, while Docker environments are not.
