### Initial Status
After a product and a device are created, the device is in **Inactive** status, and the device shadow is empty by default.


### Reporting Status by Device
After the device reports its status to IoT Hub, its latest device shadow status will be displayed in the console.


### Updating Device Shadow Status by Application
You can modify the virtual device (device shadow) in the console. After the change is saved, the device will receive the update to the virtual device.
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Products** on the left sidebar.
2. On the product list page, click the product name to enter the product details page.
3. Select **Devices**, click **Device Shadow** on the right, and click **Modify** in the top-right corner.
4. Add JSON data to the device shadow as prompted on the right. The `reported` field can be empty, while the `desired` field cannot.
5. Click **Confirm** to complete the modification.
![](https://main.qcloudimg.com/raw/f0699a528a44da440c0c877806451371.png)


