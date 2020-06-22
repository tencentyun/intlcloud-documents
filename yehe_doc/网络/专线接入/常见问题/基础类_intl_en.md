### What is Direct Connect?
[Direct Connect](https://intl.cloud.tencent.com/document/product/216/544) is a fast way to connect Tencent Cloud with your local IDC. You can apply for a connection to communicate your local IDC with Tencent Cloud computing resources in multiple regions for elastic and reliable hybrid cloud deployment.

### What does Direct Connect consist of?
Direct Connect consists of connections, dedicated tunnels, and Direct Connect gateways. For more information, please see [Product Overview](https://intl.cloud.tencent.com/document/product/216/544).
### How long does it take to apply for a connection to Tencent Cloud?

You can apply for a connection in the following steps:
- **Set up a connection**:
   - Lay fiber-optic line: this process is the **longest part in the construction period**. The laying period is subject to the connection provider's capability and connection conditions at both ends. The following are the **reference values** of laying periods in normal cases:
     - In Mainland China: 20 days for an intra-region connection and 30 days for a cross-region connection.
     - Outside Mainland China: the period varies widely by region; for example, it is 1 month for Hong Kong (China) and 1.5–2 months for regions in Europe and North America.
   - To apply for a connection by yourself, log in to the [Direct Connect Console](https://console.cloud.tencent.com/dc/dc) and enter the parameters as instructed in [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244). You need to confirm with your connection provider for some parameter settings such as port type and bandwidth.
   After your application is submitted, a Tencent Cloud Direct Connect delivery engineer will contact you to confirm your need details and initiate the construction in three days. Generally, resources such as ports and modules can be prepared in one week after construction is initiated. Then, wait for the connection provider to lay the fiber-optic line.
   - Apply through a partner: as Tencent Cloud's Direct Connect partners have been interconnected with Tencent Cloud over NNI, purchasing a connection at a partner can eliminate the need for connection construction in Tencent Cloud. You can directly create a dedicated tunnel to share the partner's connection. Therefore, you are recommended to purchase the Direct Connect service at a Tencent Cloud partner.
- **Apply for a dedicated tunnel**: submit an application in the [Tencent Cloud Console](https://console.cloud.tencent.com/dc/dcConn) as instructed in [Applying for Tunnel](https://intl.cloud.tencent.com/document/product/216/19250). After your application is submitted, the tunnel can be created in 10 minutes (if you share a partner connection, the tunnel can be created only after the application is approved by the partner).
- **Apply for a Direct Connect gateway and configure the route table**: they are both created automatically and immediately after you submit the application.

### Can a connection be used across accounts?

Yes, a connection can be used across accounts. For more information, please see [Sharing Connection](https://intl.cloud.tencent.com/document/product/216/19246).

### Can I modify the parameters after submitting a connection application?

After a connection application is submitted, you can modify the following parameters before it is pushed by the Tencent Cloud Direct Connect delivery engineer to the backend for review: ISP, access point, port type, and connection type. If you do not want to use the current application information, the engineer can reject your application, and you can submit a new application.

### What ISPs are supported by access points of Tencent Cloud Direct Connect?

Most Tencent Cloud Direct Connect access points are deployed in data centers of neutral IDC ISPs and can support access from any connection provider.
You can log in to the Direct Connect [Console](https://console.cloud.tencent.com/dc/dc), click **Create+** to create a connection, and select different ISPs to display the Direct Connect access points supporting access from the selected ISP.

### How do I find a connection provider?

You can [submit a ticket](https://console.cloud.tencent.com/workorder/category), and a Tencent Cloud Direct Connect delivery engineer will recommend an optimal connection provider for you.

### Can a connection access Tencent Cloud resources in multiple regions?

Yes, access from one point to in-cloud resources in all regions is supported in two ways:

- Tencent Cloud Direct Connect access point devices support 802.1Q VLAN encapsulation. After the trunk mode is enabled, a connection can support multiple VLANs, and you can use different VLANs to create different dedicated tunnels so as to access in-cloud VPC resources in multiple regions.
- You can also use [CCN](https://intl.cloud.tencent.com/product/ccn) to access in-cloud VPC resources in multiple regions.

### Why is the connection status always "applying"?

After you submit an application for a connection, a Tencent Cloud Direct Connect delivery engineer will confirm your need with you as soon as possible and initiate the corresponding review and construction processes. If your project is urgent, you can contact your delivery engineer or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to check the latest progress.

### How long will a connection take effect after it is approved?

It will take effect in one month. If you fail to make the payment to initiate the connection construction within one month, the connection environment will change, and the resources will be repossessed. If you still need a connection, you need to submit a new application.

### What is the purpose of the bandwidth of a connection?

The bandwidth of a connection is for record only and is not used for speed limiting. If your connection speed changes, you can contact your Tencent Cloud Direct Connect delivery engineer or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to modify the bandwidth value in the console.

### What is the "carrier circuit number" of a connection?

It is a unique circuit identifier provided by the connection provider. Please make sure that it is correct, as it is required when you locate a line with the connection provider during future line maintenance.

### Can I change the address of a connection?

- If you want to change your local IDC address, please submit your change request to your connection provider.
- If you want to change the address of the access point in Tencent Cloud, please consult your Tencent Cloud Direct Connect delivery engineer.

### Can I deploy my own devices in a Tencent Cloud data center?

No.

### Why is the dedicated tunnel status always "configuring" or "modifying"?

In normal cases, it takes several minutes to configure a new or modified dedicated tunnel. If the configuration is not completed in ten minutes, an error may have occurred during the configuration, and the backend engineer will fix it as soon as possible. You can also check the latest progress with your Tencent Cloud Direct Connect delivery engineer.

### Is Direct Connect supported outside Mainland China?

Yes. Direct Connect is supported and can be applied for in all regions displayed at Tencent Cloud's official website, and the corresponding LOA will be issued by Tencent Cloud. In regions outside Mainland China, Tencent Cloud can provide one-stop connection delivery services. For more information, please consult your Direct Connect delivery engineer.

### What are the limits for using Direct Connect?

Direct Connect resources and connections are limited. For more information, please see [Use Limits](https://intl.cloud.tencent.com/document/product/216/546).

### Is the size of transferred data limited during use of Direct Connect?

No. You can transfer data in any size, and the highest speed is the selected connection bandwidth.
For other limits, please see [Use Limits](https://intl.cloud.tencent.com/document/product/216/546).

### How do I configure alarms for a connection?

Go to the console > Cloud Monitor, click **[Create Policy](https://console.cloud.tencent.com/monitor/policycreate)**, select **Direct Connect - Connection** or **Direct Connect - Dedicated Tunnel** as the policy type, and configure the threshold alarm policy.

### What are the differences between Direct Connect and IPsec VPN Connections?

- VPN Connections uses the public network and the IPsec protocol to establish an encrypted network connection between your IDC and VPC. You can purchase a VPN gateway, make it take effect, and configure it in just a few minutes. However, a VPN connection may be closed due to public network quality problems such as internet jitters and congestion. If your business does not have a high requirement for the network connection quality, it is a cost-effective choice for rapid deployment.
- By contrast, Direct Connect provides a dedicated network connection solution, which has a long construction period but can provide high-quality and high-reliability network connection services. If your business has a high requirement for the network quality and security, you can choose Direct Connect for deployment.

For more information, please see [Product Overview](https://intl.cloud.tencent.com/document/product/216/544).

