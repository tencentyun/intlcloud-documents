[//]: # (chinagitpath:XXXXX)

## Overview
IoT Hub provides the abilities to monitor devices' online status, messaging, device shadows, rule engines and OTAs. You can view the monitoring data for the last 30 days, which helps you identify and resolve business issues.

## Status Monitoring Type
At present, five types of monitoring statistics are available, including:
- **Device online status statistics**
Device online status statistics are used to monitor the online status of the device.
![](https://main.qcloudimg.com/raw/153b377cd4d30934661e0c54cfbb6d70.png)

- **Device message statistics**
Device message statistics include the number of uplink and downlink messages and their respective failure counts and billable message counts.
![](https://main.qcloudimg.com/raw/9f837b2e2b4b4ec1a148610ca132d23f.png)
Where:
    1. The uplink message count indicates the number of messages published by the device or published by the application through the cloud API.
    2. The downlink message count indicates the number of messages transmitted by IoT Hub to the device (messages subscribed to by the device).
    3. The uplink message failure count indicates the number of messages that fail to be published due to invalid format (such as too long), frequency limit, traffic limit or permission issue among the messages that are published by the device or published by the application through the cloud API.
    4. The downlink message failure count indicates the number of messages that cannot be received due to invalid format (such as too long), frequency limit or traffic limit among the messages that are transmitted by IoT Hub to the device (messages subscribed to by the device).
    5. The billable uplink message count indicates the number of messages published by the device or published by the application through the cloud API which is converted based on the billing standard (dividing message content length by 512 bytes and rounding up to the nearest integer).
    6. The billable downlink message count indicates the number of messages transmitted by IoT Hub to the device (messages subscribed to by the device) which is converted based on the billing standard (dividing message content length by 512 bytes and rounding up to the nearest integer).

- **Device shadow update statistics**
Device shadow update statistics include the number of times the device actively updates the shadow and the number of update failures.
![](https://main.qcloudimg.com/raw/29631bbf53df34f799b3757545486eb9.png)

- **Rule engine statistics**
Rule engine statistics include the number of times the messages hit the rule engine and the number of times messages are forwarded to other services.
![](https://main.qcloudimg.com/raw/6a10b09660891ab5fa8410087831639d.png)

- **Firmware statistics**
Firmware statistics include device version and firmware version capacity.
![](https://main.qcloudimg.com/raw/22c9980c68b1f6556f91b1ea811730f7.png)


## Product-level Monitoring
Status monitoring supports not only global but also product-level monitoring. You can search by product name to find the product data you want to view.
![](https://main.qcloudimg.com/raw/a71db994dbcd5bfd6e4fecb3ad4dc166.png)
>Note: You can view firmware statistics only after specifying the product.

## Searching by Time
Status monitoring supports time range selection, including the past 1 day, 7 days, 15 days, 30 days and custom time range.
![](https://main.qcloudimg.com/raw/06c3084bf8d7395977705636ec2977aa.png)
In addition, the monitoring sequence diagram also supports scaling. You can select a start time on the sequence diagram, hold and drag the mouse to the end time to view the monitoring data for the time period.
![](https://main.qcloudimg.com/raw/ab955b960480acdea33941ab94f1c0ef.png)
