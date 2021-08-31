## Process Overview
![](https://main.qcloudimg.com/raw/9e2319ef334f7596c050816bff61c6a1.png)

The main steps in connecting an acceleration domain name to ECDN include:  

1. [Add an acceleration domain name configuration on the platform](#addhost).  
2. [Access your business with the `hosts` file to verify the business compatibility](#hosttest).  
3. [Switch the CNAME record to forward requests to ECDN](#cname).

<span id="addhost"></span>
## Step 1. Add an acceleration domain name
### 1. Enter the domain management page
 Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the **Domain Management** page. Click **Add Domain Name** to enter the **Add Domain Name** page.
 ![](https://main.qcloudimg.com/raw/676f2b9bedadc30fef163f23d5f6bfaf.png)

### 2. Enter the domain name information 
On the **Add Domain Name** page, enter the acceleration domain name information as instructed.
![](https://main.qcloudimg.com/raw/23711a3ed5c1ffdcd908f6919ce13233.png)

>!
>- If the acceleration regions are in the mainland of China, according to relevant laws and regulations, the new acceleration domain name must have been filed on record on [MIIT's ICP filing website](http://beian.miit.gov.cn/) or have obtained ICP filing through [ICP filing registration], and has not connected to Tencent Cloud CDN or ECDN before. The domain name that has been connected to the CDN needs to be deleted before being added to the ECDN platform.
>- You can manage domain names by project in the **Project** section. Here, a project is shared by all Tencent Cloud products. You can manage projects in [Project Management](https://console.cloud.tencent.com/project).
>- If the origin server type is **origin IP**, optimal route selection, weighted, and primary/secondary origin-pull policies are supported. For more information, please see configuration methods in [Advanced Origin-Pull Policies](https://intl.cloud.tencent.com/document/product/570/35821). 
>- If the origin server type is **origin domain**, you can enter only one domain name, which must be different from the acceleration domain name. You can set the port in ```Host:Port``` format, and the port number should be between 1 and 65535.
>- When you add a domain name, ECDN will display the default regular caching rules. You can modify or manage them in the rule list for customization for the domain name.

### 3. Select the origin-pull protocol
Select the transfer protocol used for communication between the edge server and origin server.
![](https://main.qcloudimg.com/raw/d39b00115568ecbfc6424fe6c6174c47.png)

### 4. Configure caching rules
Configure caching rules for dynamic and static content of the domain name. You can use the recommended configurations by default or click **Edit Caching Rule** to edit the rules.
![](https://main.qcloudimg.com/raw/5a486024219dc50972b26f1fe3527943.png)

### 5. Click "Submit"
After the domain name is configured, click **Submit** to add it. In the pop-up box, click **Go to Domain Name List** to view the domain name status. After the domain name is added, the system will deploy relevant configurations on the backend, which will take effect in about 5 minutes.
![](https://main.qcloudimg.com/raw/348c7cb0988ce42adfd55297f5b0a37b.png)
To configure the domain name with HTTPS, you can do so as instructed in [HTTPS Settings](https://intl.cloud.tencent.com/document/product/570/10365) after adding the domain name.

<span id="hosttest"></span>
## Step 2. Verify access with `hosts`
To ensure continuity of access to your business, you are recommended to set the local `hosts` file to verify whether access is normal before formally switching the CNAME resolution. If your page contains multiple dynamic domain names, you can add them in batches for verification

### 1. Get a CNAME domain name
![](https://main.qcloudimg.com/raw/6603c81e88e72f7ca2ac49c9542e7673.png)
>
> 1. Before verification with `hosts`, please make sure that the domain name is **activated**.
> 2. The CNAME address of ECDN is suffixed with ```.dsa.dnsv1.com```, which can be viewed on the **Domain Management** page.

### 2. Resolve the CNAME domain name to get the ECDN cache node IP
Run `nslookup` on the local command line to resolve the ECDN CNAME domain name so as to get the IP address of the cache node.
![](https://main.qcloudimg.com/raw/17ccbf7e5d46f1417807410dcb3e4f07.png)

### 3. Set `hosts`
You can configure the local `hosts` file to forcibly redirect access requests to the local server to the ECDN platform, so that you can verify the platform compatibility without affecting formal access to your business.  
The following uses the `hosts` file on Windows as an example to show the settings. It is generally stored in ```C:\Windows\System32\drivers\etc\hosts```:
![](https://main.qcloudimg.com/raw/cf9a029252c74f618dd1257c14f98f6c.png)

### 4. Verify access
After setting the `hosts` file, you can access resources under the acceleration domain name with a browser. The following uses Chrome as an example to show how to access the domain name:
![](https://main.qcloudimg.com/raw/06826467aa1a68135e85e28e825645a2.png)

>By using the built-in packet capture tool in the browser, you can see that:
>- The request address of the acceleration domain name is pointed to the ECDN node `113.107.216.105`. 
>- The request response status code of the acceleration domain name is `200 OK`, indicating that user requests can be responded to normally, which meets the test expectation.
>- If the response status code of the acceleration domain name is exceptional, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category). Please attach screenshots of your operations in the ticket to facilitate troubleshooting.

<span id="cname"></span>
## Step 3. Configure the CNAME record of the domain name
1. After verification with the `hosts` file is passed, you can forward requests to the domain name to the ECDN acceleration platform. You need to complete the CNAME configuration at your DNS service provider of the acceleration domain name. For more information on how to configure a CNAME record, please see [CNAME Record Configuration](https://intl.cloud.tencent.com/document/product/570/11134).
2. Check whether the CNAME record of the domain name takes effect: the time it takes for a CNAME record to take effect varies by DNS service provider. You can also run the `ping` or `dig` command to check whether the CNAME record is in effect. If a domain name suffixed with ```.dsa.sp.spcdntip.com``` or ```.dsa.p23.tc.cdntip.com``` is returned, the CNAME record has taken effect.

## Subsequent Steps
When the distribution is completed, ECDN will allocate a corresponding CNAME address to you, which needs to be configured before the acceleration service taking effect. For detailed directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/570/11134).
