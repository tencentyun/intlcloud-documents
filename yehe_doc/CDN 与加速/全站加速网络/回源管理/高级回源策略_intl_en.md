ECDN supports the following advanced origin-pull policies:  
- **[Optimal route selection origin-pull](#default)**
The best-performance origin server is selected for origin-pull based on the detection result.
- **[Weighted origin-pull](#weight)**
Requests are assigned by weight ratio for origin-pull based on the detection result.
- **[Master/slave origin-pull](#master-backup)**
The master origin server is always preferentially selected during origin-pull. The slave is selected only when the master is exceptional.

You can select an appropriate origin-pull policy based on your business needs.  
>
- The default origin-pull policy of ECDN is optimal route selection.
- Weighted and master/slave origin-pull policies support only origin servers whose type is origin server IP. Origin servers whose type is origin server domain name support optimal route selection origin-pull only.
- If weighted origin-pull is selected, the performance will also be taken into account when the platform schedules requests. Therefore, the actual origin-pull weight ratio may be different from the set ratio.
- If master/slave origin-pull is selected, the platform will monitor availability of both the master and slave origin servers. If the master is found exceptional, requests will be automatically switched to the slave and will be switched back to the master if it is found recovered.

<span id="new"></span>
## Adding Advanced Origin-Pull Policy
<span id="default"></span>
### 1. Optimal route selection origin-pull
The optimal route selection origin-pull policy is the default policy of the platform and applies to origin servers whose type is **origin server IP** or **origin server domain name**:
![](https://main.qcloudimg.com/raw/4b734146feee2ca4f83cda263f9a1787.png)

>
- If the origin server type is origin server domain name, the optimal route selection origin-pull policy will be selected by default, and you do not need to configure it. You can configure only one origin server domain name as the origin server address, which must be different from the acceleration domain name.
- If the origin server type is origin server IP, the high-quality origin-pull policy will be selected by default, and you can configure multiple origin server IP addresses.

<span id="weight"></span>
### 2. Weighted origin-pull 
Weighted origin-pull supports only origin servers whose type is **origin server IP**. You can set the origin-pull weight for different origin servers based on their loading capabilities.    
![](https://main.qcloudimg.com/raw/2645f7c578459563a5d18629f5d99a40.png)  

>
- A weight ranges from 1 to 100, and the system calculates the origin-pull ratio of different origin servers based on their weight.
- Up to 32 origin server addresses can be configured.
- If you want to add the list of ECDN origin-pull node IPs to the whitelist, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=532&source=0&data_title=动态加速网络) for application.

<span id="master-backup"></span>
### 3. Master/slave origin-pull
Master/slave origin-pull supports only origin servers whose type is **origin server IP**. You can use this feature if your want to implement origin-pull based on a master/slave architecture.
![](https://main.qcloudimg.com/raw/bce329e674245a932de6cc865ce1bb6c.png)

## Modifying Advanced Origin-Pull Policy
After adding a domain name, you can modify advanced origin-pull policies on the domain name management page in the following steps:
Step 1: log in to the [ECDN Console](https://console.cloud.tencent.com/dsa), click **Domain Management** on the sidebar, and click **Manage**.
![](https://main.qcloudimg.com/raw/6cb9dc287ebd10bcc14048a513809f62.png)

Step 2: on the **Basic Info** page, you can view the origin server configuration information. Click **Edit** to enter the editing page.
![](https://main.qcloudimg.com/raw/e6967074d11e7a5bcc9da8d65eb2a97f.png)

Step 3: in the pop-up window, you can adjust the origin server configuration as needed. For more information on how to configure advanced origin-pull policies, please see [Adding Advanced Origin-Pull Policy](#new).
![](https://main.qcloudimg.com/raw/ca8773779da3e5a00cc4f01a6b120c71.png)

>
- The origin server configuration takes 5–30 minutes to be delivered and take effect.
- When adding an origin server address, please make sure that the origin server service has been enabled; otherwise, some requests may fail after the switch.
- Before deleting an origin server address, delete the origin server configuration on the ECDN platform first and then disable the origin server service so as to reduce the risks of origin server switch.
