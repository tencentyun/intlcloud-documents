ECDN supports the following advanced origin-pull policies: 
- **[Optimal route selection origin-pull](#default)**
The best-performing origin server is selected for origin-pull based on the detection result.
- **[Weighted origin-pull](#weight)**
Requests are assigned by weight ratio for origin-pull based on the detection result.
- **[Primary/secondary origin-pull](#master-backup)**
The primary origin server is always preferentially selected during origin-pull. The secondary origin server will be selected only when the primary origin server is exceptional.

You can select an appropriate origin-pull policy based on your business needs. 
>?
>- The default origin-pull policy of ECDN is optimal route selection.
>- Weighted and primary/secondary origin-pull policies support only origin servers whose type is origin IP. Origin servers whose type is origin domain support only optimal route selection origin-pull.
>- If weighted origin-pull is selected, the performance will also be taken into account when the platform schedules requests. Therefore, the actual origin-pull weight ratio may be different from the set ratio.
>- If primary/secondary origin-pull is selected, the platform will monitor availability of both the primary and secondary origin servers. If the primary origin server returns a status code in the range of 400-599 (except for 416), requests will be automatically switched to the secondary origin server and will be switched back to the primary origin server if it is found recovered.

<span id="new"></span>
## Adding Advanced Origin-Pull Policy
<span id="default"></span>
### 1. Optimal route selection origin-pull
The optimal route selection origin-pull policy is the default policy of the platform and applies to origin servers whose type is **origin IP** or **origin domain**:
![](https://main.qcloudimg.com/raw/cb4e342444e4bf4cd00cb27d940ec9fe.png)

>?
>- If the origin server type is origin domain, the optimal route selection origin-pull policy will be selected by default, and you do not need to configure it. You can configure only one origin domain as the origin server address, which must be different from the acceleration domain name.
>- If the origin server type is origin IP, the most appropriate origin-pull policy will be selected by default, and you can configure multiple origin IP addresses.

<span id="weight"></span>
### 2. Weighted origin-pull
Weighted origin-pull supports only origin servers whose type is **origin IP**. You can set the origin-pull weights for different origin servers based on their loading capabilities.   
![](https://main.qcloudimg.com/raw/67d50247982e9eb4bcd5b244aa365f2f.png) 

>?
>- A weight ranges from 1 to 100, and the system calculates the origin-pull ratio of different origin servers based on their weights.
>- Up to 32 origin IP addresses can be configured.
>- If you want to allow the list of ECDN intermediate node IPs, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

<span id="master-backup"></span>
### 3. Primary/secondary origin-pull
Primary/secondary origin-pull supports only origin servers whose type is **origin IP**. You can use this feature if you want to implement origin-pull based on a primary/secondary architecture.
![](https://main.qcloudimg.com/raw/ec760ae6232996fe79090740a1f3812c.png)

## Modifying Advanced Origin-Pull Policy
After adding a domain name, you can modify advanced origin-pull policies on the domain management page in the following steps:
Step 1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa), click **Domain Management** on the sidebar, and click **Manage**.
![](https://main.qcloudimg.com/raw/2d636019fafbb5de9ed3e72b269b9fa9.png)

Step 2. On the **Basic Info** page, you can view the origin server configuration information. Click **Modify** to enter the editing page.
![](https://main.qcloudimg.com/raw/f6c5c81c162d7da054da02ae47ce73b3.png)

Step 3. In the pop-up window, you can adjust the origin server configuration as needed. For more information on how to configure advanced origin-pull policies, please see [Adding Advanced Origin-Pull Policy](#new).
![](https://main.qcloudimg.com/raw/7787ebc04c0657f6edda95ef0f9545e3.png)

>?
>- The origin server configuration takes 5–30 minutes to be distributed and take effect.
>- When adding an origin server address, please make sure that the origin server has been enabled for service; otherwise, some requests may fail after the switch.
>- Before deleting an origin server address, delete the origin server configuration on the ECDN platform first and then disable the origin server service so as to reduce the risks of origin server switch.
