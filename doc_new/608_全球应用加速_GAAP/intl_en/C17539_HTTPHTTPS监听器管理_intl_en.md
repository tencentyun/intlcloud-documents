## Adding a New HTTP/HTTPS Listener
1. Log into the [Global Application Acceleration Console](https://console.cloud.tencent.com/gaap). Enter the **Access Management** page. Click the **ID/Connection Name** of the specific connection.
2. On the next page, select **HTTP Listener Management**/**HTTPS Listener Management** > **Add**. You can select either HTTP or HTTPS protocol. The specific configuration is as follows:
 - When HTTP is selected, only the input port is required, and the listener will forward packets using HTTP protocol by default.
 ![](https://main.qcloudimg.com/raw/06d55770bf98cff97442729fa1a3fdba.png)
 - When HTTPS is selected, additional certificates and other information are required to be configured, as shown below:
![](https://main.qcloudimg.com/raw/a1e5c97914c65a026f95d6ac6b83e658.png)
 - **Listeners communicate with the origin server using HTTP protocol** meaning that the HTTPS protocol is used between the client and the acceleration connection VIP, while the HTTP protocol is used between the VIP and the origin server, which requires the origin server to open the HTTP protocol port. **Listeners communicate with the origin server using HTTPS protocol** meaning that the HTTPS protocol is used between the client and the origin server, and the HTTPS protocol port should be open for the origin server. The primary difference between these two options is that the link latency of the former is lower.
 - **SSL Parsing**: Only **One-way authentication** is supported, that is, server verification on the client.
 - **Server certificate**: You need to purchase a certificate in Tencent Cloud **SSL Certificate Management** or upload your own. Then you can select the corresponding certificate from the drop-down list.

## Configuring an HTTP/HTTPS Listener
Open **HTTP/HTTPS Listener Management** tab, click **Settings** in the **Operation** column to open the page for domain name and URL management.
<span id ="Adding a Rule">
### Adding a Rule</span>
In the **HTTP/HTTPS Listener Management** page, click **Add a rule** to add the domain name and corresponding URL. You can add up to 20 URL rules under the same domain name, as shown below:
1. Basic configuration
![](https://main.qcloudimg.com/raw/fcf56bdf702b67b81990cc4dedd89f0d.png)
**Domain name**: Exact match is required. It supports `a-z`, `0-9`, `_`, `.`, `–`, and can contain 3-80 characters. 
**URL**: It supports `a-z`, `A-Z`, `0-9`, `_`, `.`, `-`, `/`, and can contain 1-80 characters.
**Origin type**: Two types of origin servers are supported: IP and domain name. For the differences between the two types, see the description of TCP/UDP listener.

2. Processing policy for the origin server
Set the forwarding rules of the origin server. It supports **RR**, **Weighted RR**, and **Least Connections**. For a description of the specific policy, see the description of TCP/UDP listener.
![](https://main.qcloudimg.com/raw/bb6f7d4cf05d2fb6e623c5ed28904dbc.png)
3. Origin server health check mechanism
The monitoring check mechanism can be enabled. For the current domain name, an independent check URL can be set. The request mode supports HEAD and GET. The check status code supports http_1xx, http_2xx, http_3xx, http_4xx, and http_5xx, and one or multiple selections can be made. When the specified status code is detected, the listener considers that the backend origin server is in normal status. If no status code is detected, the listener considers that the backend origin server is abnormal.
![](https://main.qcloudimg.com/raw/20d08ec6efd43a94734b6a408afc2d10.png)

### Modifying a Domain Name
In the **HTTP/HTTPS Listener Management** page, click **Modify Domain Name** from the operation column to modify the domain name, as shown in the following figure:
![](https://main.qcloudimg.com/raw/c61efa495d61009bc93ebff1a8891de5.png)

### Deleting a Domain Name
When deleting a domain name, if a rule under the domain name is bound with the origin server, you need to check **Force deletion of rules bound with origin servers**.
![](https://main.qcloudimg.com/raw/3a7a088320acb13f1c822b1ec34c9ba1.png)

### Modifying Rules
See the preceding [Adding a Rule](#Adding a Rule) section. The main difference is that the domain name and origin server type cannot be modified.

### Binding an Origin Server
For details, see [Binding an Origin Server](https://cloud.tencent.com/document/product/608/17849#.E7.AC.AC.E5.9B.9B.E6.AD.A5.EF.BC.9A.E7.BB.91.E5.AE.9A.E6.BA.90.E7.AB.99). You can bind different ports to different origin servers.

### Deleting Rules
If there is an origin server bound under the rule, first check **Force deletion of rules bound with origin servers**.
![](https://main.qcloudimg.com/raw/2fd560217ca2f53847033d501eb90e1a.png)

## Deleting an HTTP/HTTPS Listener
Open **HTTP/HTTPS Listener Management** tab, click **Delete** in the **Operation** column to delete a specified listener. If the listener is bound with an origin server, you need to check **Allow force deletion of listeners bound with origin servers** to delete it. After deletion, acceleration service for the listener’s port stops.
![](https://main.qcloudimg.com/raw/5df2bff2fb4f07ce2631824792429147.png)

## Modifying an HTTP/HTTPS Listener
On the **HTTP/HTTPS Listener Management** tab, click **Modify** to modify the listener information.
- HTTP listener: You can modify the listener name, as shown below:
![](https://main.qcloudimg.com/raw/ea25a7af2f78c1581f137752bcd692fd.png)
- HTTPS listener: You can modify the listener name and protocol between the listener and the origin server and update the certificate, as shown below:
![](https://main.qcloudimg.com/raw/ea17d01d9ad0919e344d3e3460f63ee1.png)
