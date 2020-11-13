Tencent Cloud CLB supports the TCP, UDP, TCP SSL, HTTP, and HTTPS protocols and provides flexible forwarding capabilities based on domain names and URL paths. This document guides you through how to get started with CLB.

## Prerequisites
1. CLB only forwards traffic but cannot process requests; therefore, you need to have a CVM instance that processes user requests.
In this example, two CVM instances are enough, but you can also configure more instances. CVM instances `rs-1` and `rs-2` have been created in the Guangzhou region in this example. For more information on how to create a CVM instance, please see [Purchasing and Launching CVM Instances](https://intl.cloud.tencent.com/document/product/213/4855).
2. This document takes HTTP forwarding as an example. The corresponding web server (such as Apache, Nginx, or IIS) must be deployed on the CVM instance.
To verify the result, in this example, Nginx is deployed on both `rs-1` and `rs-2`. Nginx returns "Hello nginx! This is rs-1!" on `rs-1` and "Hello nginx! This is rs-2!" on `rs-2`. For more information on how to deploy components on a CVM instance, please see [Deploying Java Web on Linux (CentOS)](https://intl.cloud.tencent.com/document/product/214/32391) and [Installing and Configuring PHP on Windows](https://intl.cloud.tencent.com/document/product/213/10182).
3. Access the public IP and path of your CVM instances. If the deployed page is displayed, the service has been successfully deployed.
>!
> - For traditional accounts, public network bandwidth must be purchased for the CVM instances, as the bandwidth is billed by CVM rather than CLB. You can determine the account type as instructed in [Billing Overview](https://intl.cloud.tencent.com/document/product/214/36999).
>- In this example, the values returned by the service deployed on two real servers are different. In actual scenarios, to ensure that all users have a uniform experience, generally the same service should be deployed on all real servers.

## Purchasing CLB Instance
After a CLB instance is successfully purchased, the system will automatically assign it a VIP, through which CLB provides service to clients.
1. Log in to Tencent Cloud's official website and go to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. In this example, select **Guangzhou** as the region, which is the same as that of the CVM instances. Select **CLB** as the instance type, **Public Network** as the network attribute, and **Default-VPC (Default)** as the network and enter **clb-test** as the instance name.
3. Click **Buy Now** and make the payment.
For more information on CLB instances, please see [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629).
![](https://main.qcloudimg.com/raw/235e67c8fbe5878a15163e13d0c2a9b6.png)
4. On the "CLB Instance List" page, select the corresponding region to view the instance just created.
![](https://main.qcloudimg.com/raw/2c2afd943a9f6a6d03f55c00e62da8b5.png)

## Creating CLB Listener
A CLB listener forwards requests by specifying protocols and ports. This document takes configuration of forwarding HTTP client requests by CLB as an example.
### Configuring HTTP listener protocol and port
When a client sends a request, CLB will receive the request according to the listened frontend protocol and port and forward it to the real server.
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. On the instance management page, find the created CLB instance `clb-test` and click its ID to enter its details page.
3. In the "Basic Info" module, you can click the modification icon next to the instance name to rename it.
4. In **HTTP/HTTPS Listeners** in "Listener Management", click **Create** to create a CLB listener.
![](https://main.qcloudimg.com/raw/19e5ec646fcd75a5e5a817b3c6cfc0cc.png)
5. In the pop-up box, configure the following:
  - Set the name to "Listener1".
  - Set the listener protocol and port to `HTTP:80`.
6. Click **Submit** to create the CLB listener.

### Configuring listener forwarding rule
When a client sends a request, CLB will forward the request according to the configured listener forwarding rule.
1. On the "Listener Management" page, select the new listener "Listener1" and click **+** to add a rule.
![](https://main.qcloudimg.com/raw/f8ab76b69f8a0cfdd5b4332c8b80b1f2.png)
2. In the pop-up box, configure the domain name, URL path, and balancing method.
  - Domain Name: it is the domain name used by your real server, which can contain a wildcard. In this example, `www.example.com` is used. For more information, please see [Configuration Description](https://intl.cloud.tencent.com/document/product/214/9032).
  - Default Domain Name: if the client request does not match any domain name of this listener, CLB will forward the request to the default domain name. Each listener can only be configured with one default domain name. If this listener is not configured with any default domain name, CLB will forward the request to the first domain name. In this example, this field is not configured.
  - URL Path: it is the access path of your real server. `/image/` is used in this example.
  - Select "WRR" as the load balancing mode.
![](https://main.qcloudimg.com/raw/263b2486f8a5734ea8aa643ea3b34387.png)
3. Configure health check: enable health check and check the default forwarded domain name and path used by the domain name.
![](https://main.qcloudimg.com/raw/9d8c9bbe1191340e452e9feeafb20e73.png)
4. Session Persistence: do not check this option.
5. Click **Finish** to complete the listener forwarding rule configuration.
![](https://main.qcloudimg.com/raw/af7915eed019f50f8d312979637e2c34.png)

For more information on CLB listeners, please see [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151).
>!
>- A listener (i.e., listening protocol:port) can be configured with multiple domain names, and a domain name can be configured with multiple URL paths. Select a listener or domain name and click **+** to create a new rule.
>- Session persistence: if session persistence is disabled and a round-robin method is used for scheduling, requests will be assigned to different real servers in sequence; if session persistence is enabled, or it is disabled but ip_hash scheduling is used, requests will always be assigned to the same real server.

### Binding CVM instance
When a client sends a request, CLB will forward the request to the CVM instance bound to the listener for processing.
1. On the "Listener Management" page, select and expand the listener "Listener1" just created and select the domain name and URL path, and the information of the CVM instance bound to the URL path will be displayed on the right. Click **Bind**.
![](https://main.qcloudimg.com/raw/ad3bab63556a4340792b1d5dadcc1b19.png)
2. In the pop-up box, select **CVM** as the instance type, select CVM instances `rs-1` and `rs-2` in the same region as the CLB instance, set the port of the two CVM instances to "80", and keep the default weight "10" for them.
![](https://main.qcloudimg.com/raw/02a6cf1b63726a7133f97f5f56c10d74.png)
3. Click **OK** to complete binding.
4. Expand the listener to display the URL paths. You can view the bound CVM instances and their health check status. The "Healthy" status indicates that the CVM instance can properly process requests forwarded by CLB.
![](https://main.qcloudimg.com/raw/8ef5732d0748b73dd1d71b3ab0aed1d4.png)
>!A forwarding rule (listener protocol + port + domain name + URL path) can be bound to multiple ports of the same CVM instance. For example, if you deploy the same service on ports `80` and `81` on `rs-1`, CLB allows you to bind both the ports to the forwarding rule in the example, and both of them will receive the requests forwarded by CLB.

## Configuring Security Group
After creating a CLB instance, you can configure a CLB security group to isolate public network traffic. For more information, please see [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

After configuring a security group, you can choose to enable or disable "Allow Traffic by Default in Security Group" with different configurations as follows:
### Method 1. Enable "Allow Traffic by Default in Security Group"
>?This feature is currently in beta test. To try it out, please [submit a ticket](https://cloud.tencent.com/apply/p/njj5tl4a5j) for application.

For detailed directions, please see [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

### Method 2. Allow the client IP in the CVM security group
For detailed directions, please see [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

## Verifying CLB Service
After configuring a CLB instance, you can verify whether the architecture takes effect by checking whether different **domain names and URLs** under the CLB instance can access different real servers, i.e., checking whether the **content-based routing** feature is available.
### Configuring `hosts` to point the domain name to the CLB instance
1. On Windows, enter the `C:\Windows\System32\drivers\etc` directory, modify the `hosts` file, and map the domain name to the VIP of the CLB instance.
![](https://main.qcloudimg.com/raw/b12ee22250cb7c24d5e12ecb803e6355.png)
2. To check whether the `hosts` is successfully configured, run the `ping` command on the command line to check whether this domain name is successfully bound to the VIP. If data packets are returned, the binding is successful.
![](https://main.qcloudimg.com/raw/b11b20840cba86bedbaffaa424b4e021.png)
3. Enter the access path `http://www.example.com/image/` in a browser to test the CLB service. If a message is displayed as shown below, the request has been forwarded to the CVM instance `rs-1` by CLB, and the CVM instance has properly processed the request and returned the result.
![](https://main.qcloudimg.com/raw/cf61264a9406d141650ed79da21c6859.png)
4. The round robin algorithm of the listener is "weighted round robin", and the weights of the two CVM instances are both "10". If you refresh the webpage in the browser to send a new request, you can see that the request is forwarded to the CVM instance `rs-2` by CLB.
![](https://main.qcloudimg.com/raw/ab7db7b5c3952739919ae6e271bb1348.png)
>!`/` at the end of `image/` must be retained, which indicates that `image` is the default directory rather than a file named `image`.


## Configuring Redirection (Optional)
Redirection can be performed manually or automatically:
- Automatic redirection (forced HTTPS): when a PC or mobile browser accesses a web service with an HTTP request, an HTTPS response can be returned to the browser after the request passes through the CLB proxy, forcing the browser to access the webpage over HTTPS.
- Manual redirection: if you want to temporarily deactivate your web business in cases such as product sellout, page maintenance, or update and upgrade, redirection capabilities will be required. If no redirection is performed, the old address in a visitor's favorites and search engine database will return a 404 or 503 error message page, degrading the user experience and resulting in traffic waste. The SEO score obtained by this page will also become invalid.
For more information, please see [Redirection Configuration](https://intl.cloud.tencent.com/document/product/214/8839).
