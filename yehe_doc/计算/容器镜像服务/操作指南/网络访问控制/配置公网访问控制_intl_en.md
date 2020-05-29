
## Scenario

The Tencent Container Registry (TCR) Enterprise Edition supports public network access control. A whitelist can be configured to restrict clients' access to the instance through the Internet, ensuring instance data privacy and security. When a TCR Enterprise Edition instance is created, the public network access entry is disabled by default. This means you cannot use a development test server to push or pull images over the Internet.
This document describes how to configure public network access control for a TCR Enterprise Edition instance.

## Prerequisites
Before configuring public network access control for a TCR Enterprise Edition instance, you must first [create a TCR Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/35486).


## Procedure
### Opening the public network access entry
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and choose **Access Control** -> **Public network** in the left sidebar.
2. On the "Public network" page, select an instance name from the **Instance Name** drop-down list at the top of the page if you want to change the instance.
3. Select **Open Internet Access Entry** in the upper-right corner to enable the public network access entry.
When the status of this button changes from **Opening** to **Close Internet Access Entry** and **Add a Public IP Whitelist** becomes selectable, the public network access entry has been successfully enabled. See the figure below.
After the entry is enabled, all Internet access requests are still denied.



### Configuring the access policy
1. On the "Public network" page, click **Add a Public IP Whitelist** and add the public IP address range and note in the displayed window. See the figure below.

 - **Associated Instance**: target instance, for which the public network access policy is configured. You can change the instance by selecting another instance name from the "Instance Name" drop-down list at the top of the "Public network" page.
 - **Entry**: public IP address range that is allowed to access the instance. The value can be a single IPv4 address or CIDR, for example, `192.168.0.0/24`. We do not recommend that you enter `0.0.0.0/0` to accept all Internet access requests to the instance.
 - **Note**: note of the access policy. This parameter is optional.
4. Click **OK**. The public network access whitelist policy is added and takes effect.
>
>- If you need to change the whitelist information, delete the policy and create another one.
>- If the public network access entry cannot be enabled or the whitelist policy cannot be created, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
