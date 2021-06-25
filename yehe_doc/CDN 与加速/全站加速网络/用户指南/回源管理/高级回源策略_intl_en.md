ECDN supports the following advanced origin-pull policies:  
- **[Optimal origin-pull](#default)**
The best-performing origin server is selected for origin-pull based on the detection result.
- **[Weighted origin-pull](#weight)**
Requests are assigned by weight for origin-pull based on the detection result.
- **[Primary/secondary origin-pull](#master-backup)**
Your primary origin server is always a preferential option. The secondary works only if the primary is exceptional.

You can select one that is appropriate for your business needs.  
>!
- The default policy for ECDN is optimal origin-pull.
- The origin type can be set to origin IP or origin domain when you use any one of three origin-pull policies.
- The actual weight for weighted origin-pull may be slightly different from the set as your requests are being taken care of.
- In a primary/secondary origin-pull, the secondary will be automatically triggered by a status code of 400–599 (except for 416) from the primary.


## Adding Advanced Origin-Pull Policy[](id:new)

### 1. Optimal origin-pull[](id:default)
Optimal origin-pull is set as the default policy of the platform.
![](https://main.qcloudimg.com/raw/cb4e342444e4bf4cd00cb27d940ec9fe.png)

>? You cannot use the same domain name for your origin and acceleration if you set the origin type to origin domain.


### 2. Weighted origin-pull[](id:weight)
You can assign weights for different origin servers based on their loading capabilities.
![](https://main.qcloudimg.com/raw/67d50247982e9eb4bcd5b244aa365f2f.png)   

>?
- A weight ranges from 0 to 100 (all zeros not allowed), and the system calculates the origin-pull ratio of different origin servers based on their weights.
- Up to 32 origin IP addresses or domain names can be configured. A mix of two types is not accepted.
- If you want to allow the list of ECDN intermediate node IPs, you can obtain the node information with this API ecdn.tencentcloudapi.com. To ensure origin-pull success, please access the latest node information and update your whitelist within 7 days after release.


### 3. Primary/secondary origin-pull[](id:master-backup)
You can use this feature if you want to implement origin-pull based on a primary/secondary architecture.
![](https://main.qcloudimg.com/raw/ec760ae6232996fe79090740a1f3812c.png)

## Modifying Advanced Origin-Pull Policy
After adding a domain name, you can modify advanced origin-pull policies on the domain management page in the following steps:
Step 1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa), click **Domain Management** on the sidebar, and click **Manage**.
![](https://main.qcloudimg.com/raw/2d636019fafbb5de9ed3e72b269b9fa9.png)
Step 2. On the **Basic Info** page, you can view the origin server configuration information. Click **Modify** to enter the editing page.
![](https://main.qcloudimg.com/raw/f6c5c81c162d7da054da02ae47ce73b3.png)
Step 3. In the pop-up window, you can adjust the origin server configuration as needed. For more information, please see [Adding Advanced Origin-Pull Policy](#new).
![](https://main.qcloudimg.com/raw/7787ebc04c0657f6edda95ef0f9545e3.png)

>!
- The origin server configuration takes 5–30 minutes to be distributed and take effect.
- When adding an origin server address, please make sure that the origin server has been enabled for service; otherwise, some requests may fail after the switch.
- Before deleting an origin server address, delete the origin server configuration on the ECDN platform first and then disable the origin server service so as to reduce the risks of origin server switch.
