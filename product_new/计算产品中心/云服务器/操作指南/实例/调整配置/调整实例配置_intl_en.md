## Scenario
The Tencent Cloud instances' hardware devices can be adjusted easily with great flexibility. This document describes how to upgrade, degrade, or adjust instance configuration.

## Prerequisites
### Instance status
You can adjust an instance's configuration when the instance has been either started up or shut down, and the change takes effect after the instance is forced to shut down and restarted.
> **Note:**
>- When the instance has been **shut down**, you can make changes in the console directly.
-  When the instance has been **started up**, you can make changes online, and confirm forced shutdown after changes are made. The changes to configuration take effect after the instance is restarted.
- You can adjust configuration **in batch** online for multiple instances. If there is a server that has been **started up** in the batch of instances, you need to confirm the forced shutdown individually, and the changes take effect after the servers are restarted.

### Limit of configuration adjustment
- Upgrading configuration
No limit is imposed on the number of times configuration upgrade can be performed. The upgrade takes effect immediately.
- Degrading configuration
 - Postpaid instances can be degraded at any time and for unlimited times.

### Hardware 
The instances **whose system disk and data disk are both cloud disks** support adjusting configuration.

### Change of private IP
For few instances, their private IPs will change after the configuration adjustment and there will be a note on the adjustment page.

## Directions
You can upgrade the configuration of CVMs to adapt to you growing business. For all CVM types, the upgraded configuration takes effect immediately. That is, after you upgrade the configuration and pay the additional fees, the CVM will run with the new configuration immediately.

### Adjusting via console

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1)

2. For the instance to adjust, click **More** -> **Resource Adjustment** -> **Adjust Configuration**.

3. In the popup box, select the configuration you want to adjust, and then click **Next**.

4. Confirm the billing details. Click **Next**.

5. In Shutdown CVM, read the information and check **Agree to a forced shutdown**. Click **Adjust Now**.

## Adjusting via API
You can upgrade instance configuration using the APIs ResizeInstance and ResizeInstanceHour. For more information, please see [APIs for adjusting instance configuration](https://intl.cloud.tencent.com/document/product/213/33239).