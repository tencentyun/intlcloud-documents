Tencent Cloud CLB comes with various protocols such as TCP, UDP, TCP SSL, HTTP, and HTTPS, providing businesses with domain names and URL-based forwarding services. This document guides you to quickly create a CLB instance and forward client requests to two CVM instances.

## Prerequisites
1. You have created two CVM instances (this document takes **rs-1** and **rs-2** as two sample instances). For information on how to create CVM instances, please see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
2. You have deployed backend services on the two CVM instances. This document takes HTTP forwarding as an example. Nginx servers have been deployed on CVM instances **rs-1** and **rs-2**, and the two instances return two HTML static pages saying "Hello nginx! This is rs-1!" and "Hello nginx! This is rs-2!". For more information, please see [Deploying Nginx on CentOS](https://intl.cloud.tencent.com/document/product/214/32390).
>!
> - This document describes the steps for bill-by-IP accounts. For bill-by-CVM accounts, please first purchase public network bandwidth for CVM instances. If you are unsure of your account type, please see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
> - In this example, different services deployed on real servers will return different values. In practice, the services deployed on real servers are identical to provide a consistent experience for all users.

## Step 1: Purchasing a CLB Instance
After a successful purchase, the system will automatically assign a VIP to the CLB instance. The VIP will be used as the IP address to provide services to clients.
1. Log in to the Tencent Cloud console and go to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. First, select the same region as your CVM instance. Next, select **Cloud Load Balancer** as the instance type, **Public Network** as the network type. For more details, please see [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629).
>?
>- Static single-line IP is now available for beta testing. It’s supported only in Guangzhou, Shanghai, Nanjing, Jinan, Hangzhou, Fuzhou, Beijing, Shijiazhuang, Wuhan, Changsha, Chengdu, and Chongqing. 
>- To use Static single-line IP, please contact your sales rep. 
>
3. Click **Buy Now** and make a payment.
4. Return to the **Instance Management** page, select the region to see the new instance.
![](https://main.qcloudimg.com/raw/2c2afd943a9f6a6d03f55c00e62da8b5.png)

## Step 2: Configuring a CLB Listener
A CLB listener is used for forwarding through a specified protocol and port. This document demonstrates how to configure a CLB instance to forward client HTTP requests.
### Configure the HTTP listening protocol and port
When a client initiates a request, the CLB instance will receive the request according to the listening frontend protocol and port, and forward the request to the real server.
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. On the **Instance Management** page, click **Configure Listener** under the **Operation** column of the target CLB instance.
3. Select the **Listener Management** tab, click the **Create** button in the **HTTP/HTTPS Listener** section.
4. In the **Create Listener** window, please configure the following items and click **Submit**.
  - Listener name.
  - Listen protocol port (e.g., **HTTP:80**).

### Configure the listener's forwarding rule
If a client initiates a request, the CLB instance will forward the request according to the configured listener's forwarding rule.
1. In the **Listener Management** tab, click the **+** icon on the right of the new listener.
![](https://main.qcloudimg.com/raw/f8ab76b69f8a0cfdd5b4332c8b80b1f2.png)
2. In the **Create Forwarding Rules** window, configure the domain name, URL, balance method, and then click **Next**.
  - Domain name: the domain name of your real server (e.g., **www.example.com**).
  - Default domain name: if a client request does not match any listener domain names, the CLB instance will forward the request to the default domain name (default server). Each listener can be configured with only one default domain name. If a listener has no default domain name, the CLB instance will forward the request to the first domain name. This example will skip the configuration step.
  - URL: the access path to your real server (e.g., `/image/`).
  - Select **Weighted Round Robin** as the balancing method and then click **Next**. For more information, please see [Load Balancing Methods](https://intl.cloud.tencent.com/document/product/214/6153).
![](https://main.qcloudimg.com/raw/263b2486f8a5734ea8aa643ea3b34387.png)
3. Enable health check. Use the default values for both check domain and path fields, and click **Next**.
![](https://main.qcloudimg.com/raw/9d8c9bbe1191340e452e9feeafb20e73.png)
4. Disable session persistence and click **Submit**.

For more information on CLB listeners, please see [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151).
>?
>- Forwarding rules: each listener can be configured with multiple domain names, and each domain name can be configured with multiple URLs. You can select a listener or domain name, and then click the **+** icon to create new rules.
- Session persistence: if session persistence is disabled and a round-robin method is selected, requests from the same client will be assigned to different real servers in sequence; if session persistence is enabled, or it is disabled but `ip_hash` balance method is used, requests from the same client will always be assigned to the same real server.

### Bind real servers to the listener
If a client initiates a request, the CLB instance will forward the request to the CVM instance that is bound to its listener for processing.
1. In the **Listener Management** tab, click the **+** icon to expand the new listener. Click the URL, and click **Bind** in the **Forwarding Rules** section on the right.
![](https://main.qcloudimg.com/raw/ad3bab63556a4340792b1d5dadcc1b19.png)
2. In the pop-up window, select **CVM** as the instance type, select the two CVM instances **rs-1** and **rs-2** (which are in the same region as the CLB instance), set their ports to **80** and weights to **10** (the default value), and click **Confirm**.
![](https://main.qcloudimg.com/raw/02a6cf1b63726a7133f97f5f56c10d74.png)
3. [](id:qrjkjc)Now you can view the bound CVM instances and their health check status in the **Forwarding Rules** section. If the port health status is **Healthy**, the CVM instance can normally process requests forwarded by CLB instances.
![](https://main.qcloudimg.com/raw/8ef5732d0748b73dd1d71b3ab0aed1d4.png)
>!One forwarding rule (listening protocol, port, domain name, and URL) can be bound with multiple ports of the same CVM instance. If a user deploys the same service on the port **80** and **81** of **rs-1**, both ports can be bound with the sample forwarding rule and both will receive requests forwarded by the CLB instance.

## Step 3: Configuring a Security Group
After creating a CLB instance, you can configure a CLB security group to isolate public network traffic. For more information, please see [CLB Security Group Configuration](https://intl.cloud.tencent.com/document/product/214/14733).

After configuring a security group, you can enable or disable the **Allow Traffic by Default** feature:
### Method 1: Enable the Allow Traffic by Default feature
For more information, please see [CLB Security Group Configuration](https://intl.cloud.tencent.com/document/product/214/14733).

### Method 2: Allow specific client IPs on the CVM security group
For more information, please see [CLB Security Group Configuration](https://intl.cloud.tencent.com/document/product/214/14733).

## Step 4: Verifying the CLB Service
After configuring a CLB instance, you can verify whether it is effective by accessing different real servers via different **domain names and URLs** under the same CLB instance, or verifying the **Content-based Routing** feature.
### Method 1: Configure `hosts` and map the domain name to the CLB instance
1. In a Windows device, modify the **hosts** file at the directory `C:\Windows\System32\drivers\etc`, and map the domain name to the CLB instance's VIP.
![](https://main.qcloudimg.com/raw/b12ee22250cb7c24d5e12ecb803e6355.png)
2. To verify whether the **hosts** is successfully configured, you can run a **ping** command in the **cmd.exe** to test whether the domain name is successfully bound with the VIP. If there are data packs returned, they are successfully bound.
![](https://main.qcloudimg.com/raw/b11b20840cba86bedbaffaa424b4e021.png)
3. Test the CLB service by accessing http://www.example.com/image/ via a browser. If your page returns the image below, then the request has been forwarded to the CVM rs-1 by the CLB instance, and the CVM has normally processed the request and returned the service page.
![](https://main.qcloudimg.com/raw/cf61264a9406d141650ed79da21c6859.png)
4. As the balance method of the listener is weighted round robin, and the weights of the two CVM instances are 10, you can refresh the browser to initiate the request again. If your page returns the image below, the request has been forwarded to the CVM rs-2 by the CLB instance.
![](https://main.qcloudimg.com/raw/ab7db7b5c3952739919ae6e271bb1348.png)
>!The **/** in the **image/** cannot be omitted. **/** indicates that **image** is a default directory instead of a file name.

## Configuring Redirection (optional)
CLB supports automatic redirection and manual redirection. For more information, please see [Configuring Layer-7 Redirection](https://intl.cloud.tencent.com/document/product/214/8839).
- Automatic redirection (forced HTTPS): when a PC or mobile browser accesses a web service with an HTTP request, an HTTPS response is returned to the browser after the request passes through the CLB proxy, forcing the browser to access the webpage using HTTPS.
- Manual redirection: if you want to temporarily deactivate your web business in cases such as product sellout, page maintenance, or update and upgrade, you need to redirect the original page to a new page. Otherwise, the old address in a visitor's favorites and search engine database will return a 404 or 503 error message page, degrading the user experience, resulting in traffic waste, and even invalidating the accumulated scores on search engines.


## Operations
- [Deploying Java Web on CentOS](https://intl.cloud.tencent.com/document/product/214/32391) 
- [Step 2: Install and Configure PHP](https://intl.cloud.tencent.com/document/product/213/10182)
