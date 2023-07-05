## Overview
This document describes how to configure a preset maintenance authorization policy in the CVM console. You can set such a policy for all CVM instances under a tag. If a maintenance task is generated, it will be processed according to the configured preset policy with no need for your manual authorization.


## Directions
1. Log in to the CVM console and select **Maintenance Task** > **[Preset Authorization Policy](https://console.cloud.tencent.com/cvm/repair/presetrules)** on the left sidebar.
2. On the **Preset Authorization Policy** page, click **Create**.
3. In the **Create Preset Authorization Policy** pop-up window, select the specific product type, metric, and policy for preset authorization and associate tags.
4. Click **OK**. After an instance associated with a set tag generates a maintenance task, the preset policy will be used by default for maintenance.
