CDN supports configuring the IP access frequency limit to protect against CC attacks by limiting the number of access requests per second to a node allowed for a client. After the configuration is enabled, a 514 error will be returned for requests that exceed the QPS limit. Setting a lower limit may affect the use of your business by normal high-frequency users. Please set the limit according to your actual business needs.

## Configuration Guide
### Viewing the Configuration
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. In the list, find the row of the domain to be edited and click **Manage** in the operation column.
 ![](https://main.qcloudimg.com/raw/2c5a4a259daed4d3b8c9c61a3a7d187e.png)
3. Click the **Access Control** tab and configure the **IP Access Limits** module.
The “IP access limits” is disabled by default.
![](https://main.qcloudimg.com/raw/5f56595273ab87c57041b8e699761586.png)

### Modifying the IP Access Limits
1. In the **IP Access Limits** module, toggle the switch on. After that, the system will recommend a limit based on the average single-IP access requests in the last 30 days, which can be viewed in the **IP Access Limit** field below.
The default limit is calculated as follows: The number of access requests by a single IP at each of the 288 statical points per day (one point per 5 minutes) is calculated, and the 30 highest values in the last 30 days are averaged as the default limit. The default minimum limit is 10 QPS and for reference only. It is recommended to set it based on your business fluctuations.
2. Click **Edit**.
 ![](https://main.qcloudimg.com/raw/9746161eb4fd3b2e661b74df83296925.png)
3. Set the IP access limit and click **OK**.
 ![](https://main.qcloudimg.com/raw/5cae87082d8d3ace4b4e332bb06bec95.png)
 
## Configuration Case
If the domain name `www.test.com` is configured with the following IP access limit:
![](https://main.qcloudimg.com/raw/395f7053a62cf97493ab15c317338fe3.png)
Then:
- If a user with IP `1.1.1.1` requests the resource `http://www.test.com/1.jpg` for 11 times in one second, and all the access requests are made to one server on the CDN cache node A, then there will be 11 access logs generated on this server, one of which exceeds the QPS limit, and the status code “514” will be returned.
- If a user with IP `2.2.2.2` requests the resource `http://www.test.com/1.jpg` for 11 times in one second, and the access requests are evenly distributed on multiple CDN cache nodes, then each node will return the content normally.

