
## Overview

Tencent Container Registry (TCR) Enterprise Edition supports public network access control. An allowlist can be configured to restrict instance access by clients through the Internet, ensuring instance data privacy and security. When a TCR Enterprise Edition instance is created, the public network access entry is disabled by default. This means that you cannot use a development test server to push or pull images over the Internet.
This document describes how to configure public network access control for a TCR Enterprise Edition instance.

## Prerequisites
Before configuring public network access control for a TCR Enterprise Edition instance, you must first [create a TCR Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088).


## Directions
### Enabling the public network access entry
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and choose **Network ACL** > **Public network** in the left sidebar.
2. To change the instance, select the region where the desired instance is deployed and the desired instance name from the **Instance Name** drop-down list at the top of the "Public network" page.
3. Select **Open Internet Access Entry** to enable the public network access entry.
When the status of this button changes from **Opening** to **Close Internet Access Entry** and **Add a public IP to allowlist** becomes selectable, the public network access entry has been successfully enabled, as shown in the figure below.
After the entry is enabled, all Internet access requests are still denied.
![](https://main.qcloudimg.com/raw/84a4ef80fa06ea6126b7ecc40ab52a12.png)


### Configuring the access policy
1. On the "Public network" page, click **Add a public IP to allowlist** and configure the **Public IP Range** and **Note** in the window that appears, as shown in the figure below.
![](https://main.qcloudimg.com/raw/2c910090e35cd2229360ec9723a6b44d.png)
 - **Associated Instance**: target instance, for which the public network access policy is configured. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the "Public network" page.
 - **Public IP Range**: public IP address range that is allowed to access the instance. The value can be a single IPv4 address or CIDR, for example, `192.168.0.0/24`. We do not recommend that you enter `0.0.0.0/0` to accept all Internet access requests to the instance.
 - **Note**: notes about the access policy. This parameter is optional.
4. Click **OK**. The public network access allowlist policy is added and takes effect.
>?
>- To change the allowlist information, delete the policy and create another one.
>- If the public network access entry cannot be enabled or the allowlist policy cannot be created, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
