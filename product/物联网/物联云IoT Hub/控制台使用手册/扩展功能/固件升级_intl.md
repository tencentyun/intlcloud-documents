[//]: # (chinagitpath:XXXXX)

This document describes how to use the firmware upgrade service in the console.

### Adding Firmware
Enter the IoT Hub console, click **Product List** in the left pane, select the product for which to add firmware, switch to the **Firmware List** tab and click **Add Firmware**.
- The firmware version field can be 1 to 32 English letters, numbers, dots, underscores and dashes.
- The uploaded firmware file must be a .bin file or a .tar, .gz or .zip package.
- The uploaded firmware file cannot exceed 10 MB in size.
- Up to 50 pieces of firmware can be uploaded for each product. If you want to upload more, you need to delete some old ones first.

![](https://main.qcloudimg.com/raw/42e0b288cdb56948eb2ada33a789764f.png)

Once the upload is completed, the firmware will appear in the list.
![](https://main.qcloudimg.com/raw/5ad7da53f674d9a6d26b495fd2c91e0d.png)

### Single-device Upgrade
After the firmware is successfully uploaded, click **Firmware Upgrade** on the left pane, select the product for which to upgrade firmware and filter the device list by firmware version number in the drop-down box.
- The version number list displayed in the drop-down box includes all the version numbers uploaded in the console and reported by the devices.

- In this document, device "testDevice0" is created under the product "testProduct" and connected to IoT Hub backend via MQTT over TLS (asymmetric encryption) and reports its firmware version "0.0.1".

Use the firmware version drop-down list to filter out the "testDevice0" device that reports "0.0.1" and click **Upgrade firmware** to perform firmware upgrade for the single device. This function is often used for gated verification of firmware content.
![](https://main.qcloudimg.com/raw/26422264b4628f24f11a7ff7cebdd688.png)

Switch to the **Upgrade Status List** tab to view the status of the current device upgrade task.
- The status may be: device offline, task waiting, message successfully sent, downloading, downloaded, upgrading, upgrade failed, upgraded successfully.
- If the device does not report the upgraded successfully status in 15 minutes, the upgrade task will be marked as failed due to timeout.

![](https://main.qcloudimg.com/raw/154c8bae5be173a61826c61bc00be61e.png)
![](https://main.qcloudimg.com/raw/74061edf75fd436f3012a6f382e55fb5.png)
![](https://main.qcloudimg.com/raw/e93de2173d654ddc8e871ed4f3fa8ba6.png)
### Batch Upgrade
After the firmware is successfully uploaded, click **Firmware Upgrade** on the left pane, select the product for which to upgrade firmware, filter the device list by firmware version number in the drop-down box and click **Batch Upgrade Firmware**.
![](https://main.qcloudimg.com/raw/48db77076fc849684c2eed7b4a7ff34a.png)

Switch to the **Upgrade Status List** tab to view the current upgrade status of all the devices in the batch upgrade task.
![](https://main.qcloudimg.com/raw/154c8bae5be173a61826c61bc00be61e.png)

