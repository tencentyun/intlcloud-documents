
## Overview

Tencent Container Registry (TCR) Enterprise supports public network access control. An allowlist can be configured to restrict instance access by clients through the Internet, ensuring instance data privacy and security. When a TCR Enterprise instance is created, the public network access entry is disabled by default. This means that you cannot use a development test server to push or pull images over the internet.
This document describes how to configure public network access control for a TCR Enterprise instance.

## Prerequisites
Before configuring public network access control for a TCR Enterprise instance, you must [create a TCR Enterprise instance](https://intl.cloud.tencent.com/document/product/1051/35486).


## Directions
### Enabling the public network access entry
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Network ACL** > **Public network** in the left sidebar.
2. To change the instance, select the region where the desired instance is deployed and the desired instance name from the **Instance name** drop-down list at the top of the "Public network" page.
3. Select **Open internet access entry** to enable the public network access entry.
When the status of the button changes from **Enabling** to **Close internet access entry**, and **Add a public IP to allowlist** is in a selectable status, it indicates that the entry is enabled, as shown in the following figure.
After the entry is enabled, all internet access requests are still denied.
![](https://qcloudimg.tencent-cloud.cn/raw/2745abc93502f3d3eea4a214ecb4c8f0.png)


### Configuring the access policy
1. On the “Public network” page, click **Add a public IP to allowlist**. Configure the public IP range and notes in the pop-up window.
   - **Associated instance**: The target instance, for which the public network access policy is configured. To change the instance, select the desired instance name from the "Instance name" drop-down list at the top of the "Public network" page.
   - **Method**: You can manually configure public IP addresses or import the public IP list from an existing security group.
     - **Manually configure**: The public IP address range that is allowed to access the instance. The value can be a single IPv4 address or CIDR block, for example, `192.168.0.0/24`. We do not recommend that you enter `0.0.0.0/0` to accept all internet access requests to the instance.
     - **Import existing**: All allowed addresses in the inbound rules will be deduplicated and imported to the allowlist. After importing, you can further modify the list manually. Please note that the modified security group configurations cannot be synced automatically, and you need to re-import them again.
   - **Note**: Notes about the access policy. This parameter is optional.
2. Click **OK**. The public network access allowlist policy is added and takes effect.


If the public network access entry cannot be enabled or the allowlist policy cannot be created, you can [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).

