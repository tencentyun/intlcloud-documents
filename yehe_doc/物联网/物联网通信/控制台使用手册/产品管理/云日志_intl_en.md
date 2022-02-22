
The cloud log module of IoT Hub provides a comprehensive, stable, and reliable log service that logs information in multiple dimensions such as device behavior, message content, and device exception. You can search for key device logs by time, log type, result, device name, `RequestID`, and keyword to identify and troubleshoot business issues easily.

## Directions

1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Products** on the left sidebar to enter the product list page.
2. Click the name of the target product to enter the product details page.
3. Click **Cloud Log** to enter the log management page.

## Running Log

Running logs are divided into behavior logs, content logs, and device logs. You can search for logs by time and keyword.
- **Search by time**
You can select the time range during which to view logs on the time panel, including the last 15 minutes, last hour, last 4 hours, last 24 hours, and custom time range. **Cloud logs can be stored for up to 7 days**.
- **Search by keyword**
In the log search box, you can filter the logs to be queried. When you need to filter target logs by multiple conditions, you can press Enter to separate different tags.

### Behavior logs
You can search for logs of all communication behaviors between a device and the cloud, including device connection, disconnection, publishing, and subscribing.
![](https://main.qcloudimg.com/raw/b3b6fd1ae47e0ac174defb9317a77a9d.png)

### Content logs
You can search for detailed logs of communication content between a device and the cloud.
![](https://main.qcloudimg.com/raw/aa083f6fd7798bc8cc531539311a9557.png)

### Device logs
Device logs display device information at four levels: ERROR, WARN, INFO, and DEBUG. You can enable/configure device log collection on the device details page.
![](https://main.qcloudimg.com/raw/56070913c36a631da3a37550ddf60fba.png)



## Loading More
A cloud log loads 100 data entries each time. You can click **Load More** at the bottom of the page to view more log information.


## Log Dump

By configuring CLS, you can dump cloud log data to CLS for permanent storage and log analysis.
>!Access to the following services requires authorization and may incur fees.
>
During the initial configuration, click **Configure** > **Authorize** to enter the role page in CAM and click **Authorize**.
![](https://main.qcloudimg.com/raw/ff3c65ee65376fced87fc4435d4e1a7f.png)
