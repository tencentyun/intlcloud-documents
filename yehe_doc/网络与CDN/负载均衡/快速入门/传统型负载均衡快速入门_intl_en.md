This document describes how to create a public network Classic CLB instance named `clb-test` and forward requests from clients to two real servers.

## Prerequisites
1. CLB only forwards traffic but cannot process requests; therefore, you need to have a CVM instance that processes user requests.
In this example, two CVM instances are enough, but you can also configure more instances. CVM instances `rs-1` and `rs-2` have been created in the Guangzhou region in this example. For more information on how to create a CVM instance, please see [Purchasing and Launching CVM Instances](https://intl.cloud.tencent.com/document/product/213/4855).
2. This document takes HTTP forwarding as an example. The corresponding web server (such as Apache, Nginx, or IIS) must be deployed on the CVM instance.
To verify the result, in this example, Apache is deployed on both `rs-1` and `rs-2`. Apache returns "Hello Tomcat! This is rs-1!" on `rs-1` and "Hello Tomcat! This is rs-2!" on `rs-2`. For more information on how to deploy components on a CVM instance, please see [Deploying Java Web on Linux (CentOS)](https://intl.cloud.tencent.com/document/product/214/32391) and [Installing and Configuring PHP on Windows](https://intl.cloud.tencent.com/document/product/213/10182).
3. Access the public IP and path of your CVM instances. If the deployed page is displayed, the service has been successfully deployed.
>!
> - For traditional accounts, public network bandwidth must be purchased for the CVM instances, as the bandwidth is billed by CVM rather than CLB. You can determine the account type as instructed in [Billing Overview](https://intl.cloud.tencent.com/document/product/214/36999).
>- In this example, the values returned by the service deployed on two real servers are different. In actual scenarios, to ensure that all users have a uniform experience, generally the same service should be deployed on all real servers.

## Purchasing Classic CLB Instance
1. Log in to Tencent Cloud's official website and go to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. In this example, select **Guangzhou** as the region, which is the same as that of the CVM instances. Select **Classic** as the instance type, **Public Network** as the network attribute, and **Default-VPC (Default)** as the network and enter "clb-test" as the instance name.
3. Click **Buy Now** and make the payment. For more information on CLB instances, please see [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629).
4. On the "CLB Instance List" page, select the corresponding region to view the instance just created.
![](https://main.qcloudimg.com/raw/183ac407a68c4aafe440aa2c111a154e.png)

## Creating CLB Listener
A CLB listener forwards requests by specifying protocols and ports. This document takes configuration of forwarding HTTP client requests by CLB as an example.
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. In the "CLB Instance List", find the created Classic CLB instance `clb-test` and click its ID to enter its details page.
3. In the "Basic Info" section, you can click "Edit" next to the instance name to rename it.
4. In **Listeners** in "Listener Management", click **Create** to create a CLB listener.
![](https://main.qcloudimg.com/raw/df7de6ac8996718bc5176b14f25cd3cb.png)
5. In the pop-up box, configure the following:
  - Set the name to "Listener1".
  - Set the listener protocol and port to `HTTP:80`.
  - Set the backend port to `80`.
  - Select "WRR" as the load balancing mode.
  - Do not check session persistence.
  - Enable health check.
  ![](https://main.qcloudimg.com/raw/41cbc18c096ed2f6c01a238dc426963e.png)
6. Click **Complete** to create the CLB listener.

For more information on CLB listeners, please see [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151).

## Binding Real Server
1. In the "CLB Instance List", find the created `clb-test` and click its ID to enter its details page.
2. In the "Bind Real Server" module in "Listener Management", click **Bind**.
![](https://main.qcloudimg.com/raw/a1c1ba2fa1b95a27a534a2446c381fc3.png)
3. In the pop-up box, select CVM instances `rs-1` and `rs-2` in the same region as the CLB instance and keep the default weight "10" for them.
4. Click **OK** to complete binding.
![](https://main.qcloudimg.com/raw/0c9f911e40621ff3615ac47d94651329.png)
5. Expand the listener **Listener1**. You can view the health check status of the backend CVM instance. The "Healthy" status indicates that the CVM instance can properly process requests forwarded by CLB.


## Configuring Security Group
After creating a CLB instance, you can configure a CLB security group to isolate public network traffic. For more information, please see [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).
After configuring a security group, you can choose to enable or disable "Allow Traffic by Default in Security Group" with different configurations as follows:

### Method 1. Enable "Allow Traffic by Default in Security Group"
>?This feature is currently in beta test. To try it out, please submit a ticket for application. This feature is not supported for classic private network CLB.
>
For detailed directions, please see [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).


### Method 2. Allow the client IP in the CVM security group
For detailed directions, please see [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

## Verifying CLB Service
1. Enter the CLB service address and port `http://vip:80` in a browser to test the CLB service. If a message is displayed as shown below, the request has been forwarded to the CVM instance `rs-1` by CLB, and the CVM instance has properly processed the request and returned the result.
![](https://main.qcloudimg.com/raw/5a7cb3e86d04149978b90050546a2983.png)
2. The round robin algorithm of the listener is "weighted round robin", and the weights of the two CVM instances are both "10". If you refresh the webpage in the browser to send a new request, you can see that the request is forwarded to the CVM instance `rs-2` by CLB.
![](https://main.qcloudimg.com/raw/8f9f5f667461a5d0efd3e6b2bbe859f3.png)
>!
>- If session persistence is disabled and a round-robin method is used for scheduling, requests will be assigned to different real servers in sequence.
>- If session persistence is enabled, or it is disabled but ip_hash scheduling is used, requests will always be assigned to the same real server.
