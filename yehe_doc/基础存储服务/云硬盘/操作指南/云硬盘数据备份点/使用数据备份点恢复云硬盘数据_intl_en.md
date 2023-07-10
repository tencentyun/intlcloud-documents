## Overview

The data backup point of a cloud disk provides continuous data backup service for the cloud disk. When you have the data backup point, you can restore cloud disk data to a historical time point to mitigate data loss caused by viruses, intrusions, and maloperations. This document describes how to restore cloud disk data to a backup time point with an existing data backup point.

## Notes
Keep the following in mind when using the data backup point to restore data:
- You need to shut down the CVM instance. As this will affect business continuity, we recommend you make preparations and perform the operation during off-peak hours.
- The operation will clear cloud disk data after the data backup point. Evaluate the impact in advance.


## Directions
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs/index) and select the target region at the top of the page.
2. Find the target cloud disk in the list and click **ID/Name** to enter its details page.
3. On the details page, select the **Historical Data Backup Point** tab, find the target data backup point, and click **Roll back to Backup Point** on the right.

4. In the **Roll back to Backup Point** pop-up window, confirm the information. If the CVM instance to which the cloud disk is attached is running, you also need to indicate your consent to CVM shutdown.
5. Click **OK**.

