## Creating an HTTP/HTTPS Listener
1. Log into the [GAAP Console](https://console.cloud.tencent.com/gaap). Enter the **Access Management** page. Click **ID/Connection Name** of a specified connection.
2. On the next page, select **HTTP/HTTPS listener management** > **Create**. You can select either HTTP or HTTPS protocol. The specific configuration is as follows:
 - If HTTP is selected, only the port number is required, and the listener will forward packets using the HTTP protocol by default.
 ![](https://main.qcloudimg.com/raw/0096d45b44fbd916012317a49a97a884.png)
 - If HTTPS is selected, certificates and additional information need to be configured, as shown below:
![](https://main.qcloudimg.com/raw/941665ba354633d345929e3fbd02fa8c.png)
 - **Listeners communicate with the origin server using HTTP protocol** means the HTTPS protocol is used between the client and the acceleration connection VIP, while the HTTP protocol is used between the VIP and the origin server, which requires the origin server to open an HTTP port. **Listeners communicate with the origin server using HTTPS protocol** means the HTTPS protocol is used between the client and the origin server, which requires the origin server to open an HTTPS protocol port. The main difference between the two options is that the former has lower linkage latency.
 - **SSL Parsing**: Both one-way and two-way authentication are supported.
 - **Server Certificate**: You need to purchase a certificate in Tencent Cloud **SSL Certificates Management** or upload your own. Then, select the corresponding certificate from the drop-down list.

## Configuring an HTTP/HTTPS Listener
Under the **HTTP/HTTPS listener management** tab, click **Set a rule** in the operation column to enter the domain name and URL management page.
<span id ="Add a rule"></span>
### Adding a rule
On the "HTTP/HTTPS listener management" page, click **Add a Rule** to add a domain name and the corresponding URL. You can add up to 20 URL rules under one domain name, as shown below:
1. Basic Configuration
![](https://main.qcloudimg.com/raw/fcf56bdf702b67b81990cc4dedd89f0d.png)
**Domain Name**: Exact match is required. It supports `a-z`, `0-9`, `_`, `.`, `–` and can contain 3-80 characters.
**URL**: It supports `a-z`, `A-Z`, `0-9`, `_`, `.`, `-`, `/` and can contain 1-80 characters.
**Origin Server Type**: Two types of origin servers are supported: IP and domain name. For differences between these two types, see the description of TCP/UDP listener.

2. Processing policy for origin server
Configure the forwarding rules of the origin server. It supports "RR", "Weighted RR", and "Least Connections". For policy details, see the description of TCP/UDP listener.
![](https://main.qcloudimg.com/raw/bb6f7d4cf05d2fb6e623c5ed28904dbc.png)
3. Origin server health check mechanism
The health check mechanism can be enabled. For the current domain name, you can configure an independent check URL. HEAD and GET request methods are supported. Check status codes include http_1xx, http_2xx, http_3xx, http_4xx, and http_5xx, and one or multiple codes can be selected. When a specified status code is detected, the listener considers that the backend origin server is normal. If no status code is detected, the listener considers that the backend origin server has an exception.
![](https://main.qcloudimg.com/raw/20d08ec6efd43a94734b6a408afc2d10.png)

### Modifying a domain name
On the **HTTP/HTTPS listener management** page, click **Modify domain name** in the operation column to modify a domain name, as shown below:
![](https://main.qcloudimg.com/raw/c61efa495d61009bc93ebff1a8891de5.png)

### Deleting a domain name
When you delete a domain name, if a rule under the domain name is bound with an origin server, you need to check **Force deletion of rules bound with origin server**.
![](https://main.qcloudimg.com/raw/3a7a088320acb13f1c822b1ec34c9ba1.png)

### Modifying a rule
Please see the [Adding a rule] section above. The main difference is that the domain name and origin server type cannot be modified.

### Binding an origin server
For more information, see [Binding an origin server](https://intl.cloud.tencent.com/document/product/608/17849). You can bind different ports to different orgin servers.

### Deleting a rule
If the rule is bound with an origin server, first check **Force deletion of rules bound with origin server**.
![](https://main.qcloudimg.com/raw/2fd560217ca2f53847033d501eb90e1a.png)

## Deleting an HTTP/HTTPS listener
Open the **HTTP/HTTPS listener management** tab, click **Delete** in the operation column of the specified listener to be deleted. If the listener is bound with an origin server, you need to check **Allow force deletion of listeners bound with origin servers** first. After deletion, acceleration service for the listener's port stops.
![](https://main.qcloudimg.com/raw/5df2bff2fb4f07ce2631824792429147.png)

## Modifying an HTTP/HTTPS listener
Open the **HTTP/HTTPS listener management** tab, click **Modify configuration** to modify listener information.
- HTTP listener: You can modify the listener name, as shown below:
![](https://main.qcloudimg.com/raw/d5b29fcb1b890469d1e023402d90675e.png)
- HTTPS listener: You can modify the listener name, the protocol between the listener and origin server, and update the certificate, as shown below:
![](https://main.qcloudimg.com/raw/d25c42f99371c5f486b30e22c5789451.png)
