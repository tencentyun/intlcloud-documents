## Overview

**Cross-region Copying** allows you to quickly deploy the same CVM instances in different regions. Deploying the same CVM instance in different regions using image synchronization is a reliable way to improve application robustness.

## Synchronizing images to different regions on Console
1) Log in to [CVM Console](https://console.cloud.tencent.com/cvm/).

2) Click **Image** in the navigation pane.

3) Check the image you want to copy, click **More** > **Cross-region copying**.

4) Select the destination region, and click **OK**.

5) After successful synchronization, the image list status in the destination region is updated to 100%.

## Synchronize images to different regions via API
You can use the SyncCvmImage API to synchronize images. For details, refer to [SyncCvmImage API](https://intl.cloud.tencent.com/doc/api/229/1336).
