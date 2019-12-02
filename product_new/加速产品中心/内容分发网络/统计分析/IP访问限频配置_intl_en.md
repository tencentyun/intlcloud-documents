CDN supports configuring the IP access frequency limit to protect against CC attacks by limiting the number of access requests per second to a node allowed for a client. After the configuration is enabled, a 514 error will be returned for requests that exceed the QPS limit. Setting a lower limit may affect the normal usage of high-frequency users. Please set the limit according to your actual business needs.

## Configuration Guide
### Viewing the Configuration
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. Find the domain name you want to edit and click **Manage** in the operation column.
 ![](https://main.qcloudimg.com/raw/9158bfbd91507029bb1e3db6803a1902.jpg)
3. Click the **Access Control** tab and configure the **IP Access Limits** module.
The “IP Access Limits” feature is disabled by default.
![](https://main.qcloudimg.com/raw/b1a47c98966b54ba3b7f567fcd7e77d1.jpg)

### Modifying the IP Access Limits
1. Go to the **IP Access Limits** module and toggle the switch on. The system will automatically input a default limit based on the average single-IP access requests in the last 30 days. You can view this limit in the **IP Access Limit** field below.
The default limit is calculated as follows: The number of access requests by a single IP at each of the 288 statical points per day (one point per 5 minutes) is calculated, and the 30 highest values in the last 30 days are averaged as the default limit. The default minimum limit is 10 QPS and for reference only. We recommend setting the limit based on your business fluctuations.
2. Click **Edit**.
 ![](https://main.qcloudimg.com/raw/12435984cc9021f8bce8a461b6771a26.jpg)
3. Set the IP access limit and click **OK**.
 ![](https://main.qcloudimg.com/raw/59df44ccb581aaf4ba85fa336352e2fe.jpg)
 
## Sample Case
If the domain name `www.test.com` is configured with the following IP access limit:
![](https://main.qcloudimg.com/raw/12435984cc9021f8bce8a461b6771a26.jpg)
Then:
- If a user with IP `1.1.1.1` requests the resource `http://www.test.com/1.jpg` for 11 times in one second, and all the access requests are made to one server on the CDN cache node A, then there will be 11 access logs generated on this server, one of which exceeds the QPS limit, and the status code “514” will be returned.
- If a user with IP `2.2.2.2` requests the resource `http://www.test.com/1.jpg` for 11 times in one second, and the access requests are evenly distributed on multiple CDN cache nodes, then each node will return the content.

