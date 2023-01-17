## Overview
After the component configuration is modified, saved, and delivered, you can view the configuration status to check for service configuration delivery failures or configuration expiration. You can view the configuration failure and expiration details to understand the modified configuration items of each role.
## Specification items
Synced: No configuration item is modified, or the service is restarted after the modification.
Configuration expired: The service is not restarted after the configuration item is modified and delivered, which means the configuration does not take effect.
Configuration failed: The modified configuration item fails to be delivered to the node configuration.
## Status
1. A role instance has three configuration statuses: **Synced**, **Configuration failed**, and **Configuration expired**.
	- The initial configuration status is **Synced**. If the role process configuration fails to be delivered, the configuration status of the role will become **Configuration failed**.
	- After the configuration is delivered successfully, the configuration status of the role will become **Configuration expired**.
	- In the absence of a configuration failure, the configuration status of the role will become **Synced** after the service is restarted successfully.
2. A client has two configuration statuses: **Synced** and **Configuration failed**.
	- The initial configuration status is **Synced**. If the client configuration or role process configuration fails to be delivered, the configuration status of the client will become **Configuration failed**.
	- After the configuration is delivered successfully, the configuration status of the client will become **Synced**.
3. A component has two configuration statuses: **Configuration failed** and **Configuration expired**.
	- The initial status is not displayed. If the role instance or client fails to be configured, the configuration status of the component will become **Configuration failed**.
	- If the role instance configuration expires, the configuration status of the component will become **Configuration expired**.
	- If the role instance or client has both failed configuration and expired configuration, the configuration status of the component will be displayed as **Configuration failed**.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Service** and click the component block whose configuration status is **Configuration failed** or **Configuration expired**.
3. Here takes **Configuration expired** as an example. On the component details page, click the configuration status icon in the top-right corner to view the expired configuration details.
![](https://qcloudimg.tencent-cloud.cn/raw/c75eea5ab42afc836f0ee7eeee84cf40.png)
4. Confirm the target expired configuration and restart the service.