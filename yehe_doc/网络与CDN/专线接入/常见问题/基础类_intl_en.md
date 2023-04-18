**Direct Connect FAQs**
- [What is Direct Connect?](#01)
- [What does Direct Connect consist of?](#02)
- [How long does it take to apply for Tencent Cloud Direct Connect?](#03)
- [Is Direct Connect supported outside the Chinese mainland?](#05)
- [What are the use limits of Direct Connect?](#06)
- [Is there any data transmission limit for Direct Connect?](#07)
- [What are the differences between Direct Connect and IPsec VPN?](#08)
- [Can Direct Connect be used across accounts?](#51)
- [How do I configure alarm policies for Direct Connect?](#32)

**Carrier FAQs**
 [Which carriers can access the Tencent Cloud Direct Connect access point?](#21)

**Connection FAQs**
- [Can I modify the parameters of a submitted connection application?](#11)
- [Can a connection access Tencent Cloud resources in multiple regions?](#12)
- [Why does the connection stuck in the **Applying** status?](#13)
- [When will the connection take effect after it is approved?](#14)
- [What is the bandwidth of the connection used for?](#15)
- [What is the **carrier circuit ID** of a connection?](#16)
- [Can I change the address of a connection?](#17)
- [Can I deploy my CPE in a Tencent Cloud data center?](#18)

- **Dedicated Tunnel FAQs**
- [Why does the dedicated tunnel stuck in the **Configuring** or **Modifying** status?](#31)
- [Notice on the shared connection deactivation](#04)

**Compliance FAQs**
- [Can I continue using the shared connection?](#67)
- [Why should I choose legitimate private line service](#68)
- [Why is a legitimate line access is necessary for Tencent Cloud?](#69)
- [What are the consequences of using illegal private line service?](#70)

<span id ="01"></span>

### What is Direct Connect?

[Direct Connect](https://intl.cloud.tencent.com/document/product/216/544) provides a fast and secure connection from on-premises IDCs to Tencent Cloud. You can access Tencent Cloud computing resources in multiple regions and use the connection to implement flexible and reliable hybrid cloud deployments.

<span id ="02"></span>

### What does Direct Connect consist of?

Direct Connect consists of connection, dedicated tunnel, and direct connect gateway. For more information, see [Product Overview](https://intl.cloud.tencent.com/document/product/216/544).
<span id ="03"></span>

### How long does it take to apply for Tencent Cloud Direct Connect?

To apply for Tencent Cloud Direct Connect, complete the following tasks:

- **Establish a connection**:
  - Leased line is really **time-consuming**. The construction period depends on the connection provider’s capability and access conditions on both sides of Direct Connect. The normal **reference period** is as follows:
    - In the Chinese mainland: it takes 20 days to establish an intra-region connection and 30 days to establish an inter-region connection.
    - Outside the Chinese mainland: the period varies widely by region. For example, a connection in Hong Kong (China) takes 1 month while that in Europe and North America regions takes 1.5-2 months.
  - Apply for a connection by yourself: log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and submit an application as instructed in [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244). You need to confirm with your connection provider for some parameter settings such as port type and bandwidth.
    After your application is submitted, a Tencent Cloud Direct Connect delivery engineer will check with you the details of your needs and initiate the construction in three business days. Generally, resources including ports and components can be prepared in one week after construction is initiated. Then the connection provider can start the optic fiber access.
  - Apply for a connection through a partner: as Tencent Cloud's Direct Connect partners have been interconnected with Tencent Cloud over NNI, purchasing a connection from these partners can eliminate the need for connection construction in Tencent Cloud. This way allows you to easily create a dedicated tunnel to share the partner's connection. Therefore, we recommend you purchase the connection from a Tencent Cloud partner listed in [Tencent Cloud Market](https://market.cloud.tencent.com/categories/1042).
- **Apply for a dedicated tunnel**: submit an application in the [Tencent Cloud console](https://console.cloud.tencent.com/dc/dcConn) as instructed in [Applying for a Tunnel](https://intl.cloud.tencent.com/document/product/216/19250). After your application is submitted, the tunnel will be created in 10 minutes (if you share a partner’s connection, the tunnel will be created only after your application is approved by the partner).
- **Apply for a direct connect gateway and configure the route table**: they are both created automatically and immediately after you submit the application.

<span id ="51"></span>

### Can Direct Connect be used across accounts?
Yes. The shared connection feature allows you to use a connection across accounts, but a new tunnel (including dedicated tunnels and Internet tunnels) no longer supports this feature since August 1, 2020 at 00:00:00.
- If you want to use Direct Connect service, you can connect to Tencent Cloud by [applying for a dedicated tunnel](https://intl.cloud.tencent.com/document/product/216/19250). For more information on access methods, contact your Tencent Cloud sales rep.
- If you have used the shared connection and deleted one, the quota of the shared tunnel will be deducted. For example, assume that you applied for 3 shared tunnels to bind to a connection, you can bind up to 2 tunnels after you deleted the shared tunnel 1.

<span id ="11"></span>

### Can I modify the parameters of a submitted connection application?

Before the connection application you submitted is reviewed, you can modify the following parameters: carrier, access point, port type, and connection type. If you no longer need this application, you can request the engineer to reject it, and you can submit a new one.

<span id ="21"></span>

### Which carriers can access the Tencent Cloud Direct Connect access point?

Most Tencent Cloud Direct Connect access points are deployed in neutral IDCs and support access from any connection provider.
To view the supported Direct Connect access points, log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc), click **+New** to create a connection, and select a connection provider.

<span id ="22"></span>

### How can I locate a connection provider?

You can search the [Tencent Cloud Market](https://market.cloud.tencent.com/categories/1042) for a right provider or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to obtain the recommended provider.

<span id ="12"></span>

### Can a connection access Tencent Cloud resources in multiple regions?

Yes. You can use a connection to access cross-region cloud resources in the following two ways:

- Devices at Tencent Cloud Direct Connect access points support 802.1Q VLAN encapsulation. After the Trunk mode is enabled, a connection can support multiple VLANs, and you can use different VLANs to create different dedicated tunnels so as to access cloud VPC resources in multiple regions.
- Add these VPCs to a [CCN](https://www.tencentcloud.com/products/ccn).

<span id ="13"></span>

### Why does the connection stuck in the **Applying** status?

After you submit an application for a connection, a Tencent Cloud Direct Connect delivery engineer will check with you the details and initiate the corresponding review and construction processes. If your project is urgent, you can contact your delivery engineer or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to get the latest progress.

<span id ="14"></span>

### When will the connection take effect after it is approved?
It will take effect in one month. However, if the payment is not made within one month, the connection environment may change, and the resources will be repossessed. If you still need a connection, reapply for approval.

<span id ="15"></span>

### What is the bandwidth of the connection used for?
The bandwidth of a connection is for record only and irrelevant to speed limit. If your connection speed changes, you can contact your Tencent Cloud Direct Connect delivery engineer or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to modify the bandwidth value in the console.

<span id ="16"></span>

### What is the **carrier circuit ID** of a connection?
It is the unique circuit identifier provided by the connection provider. Ensure its correctness, as it is required for your future troubleshooting of this line with the connection provider.

<span id ="17"></span>

### Can I change the address of a connection?
- If you want to change the address of your local IDC, contact your  connection provider.
- If you want to access another Tencent Cloud access point, please consult your Tencent Cloud Direct Connect delivery engineer.

<span id ="18"></span>

### Can I deploy my CPE in a Tencent Cloud data center?
No, it's not.

<span id ="31"></span>

### Why does the dedicated tunnel stuck in the **Configuring** or **Modifying** status?
It takes several minutes to create or modify a dedicated tunnel. If the configuration is not completed in ten minutes, our engineer will fix it. You can also contact your Direct Connect delivery engineer to stay informed.


<span id ="04"></span>

### Notice on the shared connection deactivation
Yes. The shared connection feature allows you to use a connection across accounts, but a new tunnel (including dedicated tunnels and internet tunnels) no longer supports this feature since August 1, 2020 at 00:00:00.
- If you want to use Direct Connect service, you can connect to Tencent Cloud by [applying for a dedicated tunnel](https://intl.cloud.tencent.com/document/product/216/19250). For more information on access methods, contact your Tencent Cloud sales rep.
- If you have used the shared connection and deleted one, the quota of the shared tunnel will be deducted. For example, assume that you applied for 3 shared tunnels to bind to a connection, you can bind up to 2 tunnels after you deleted the shared tunnel 1.

<span id ="05"></span>

### Is Direct Connect supported outside the Chinese mainland?

Yes. Direct Connect is available in all Tencent Cloud regions. The corresponding LOA will be issued by Tencent Cloud. In regions outside the Chinese mainland, Tencent Cloud provides one-stop connection delivery services. For more information, consult your Direct Connect delivery engineer.

<span id ="06"></span>

### What are the use limits of Direct Connect?

There are limits on resources and access of Direct Connect. For more information, please see [Service Limits](https://intl.cloud.tencent.com/document/product/216/546).

<span id ="07"></span>

### Is there any data transmission limit for Direct Connect?

No. You can transfer data in any size, and the highest speed is the selected connection bandwidth.
For more information, please see [Service Limits](https://intl.cloud.tencent.com/document/product/216/546).

<span id ="32"></span>

### How do I configure alarm policies for Direct Connect?

For more information, please see [Configuring Alarm Policies](https://intl.cloud.tencent.com/document/product/216/38402).


<span id ="08"></span>

### What are differences between Direct Connect and IPSec VPN connections?

- A VPN connection establishes an encrypted network connection between your IDC and VPCs based on the public network and IPsec protocol. You can purchase a VPN gateway and make it effective in just a few minutes. However, a VPN connection may be interrupted due to public network jitters or congestion. If your business does not require a high-quality network connection, the VPN connection is a cost-effective choice for rapid deployment.
- Direct Connect provides a dedicated network connection solution that features high quality and reliability, although its construction takes a longer time. If your business requires high network quality and security, you can choose Direct Connect for deployment.

For more information, see [Product Overview](https://intl.cloud.tencent.com/document/product/216/544).



<span id ="67"></span>
- Can I continue using the shared connection?
Yes. But if you delete the shared connection, you cannot reapply after August 1, 2020 at 00:00:00.

<span id ="68"></span>
### Why should I choose legitimate private line service?
As required by the national laws, regulations and [MITT Telecom Service Catalog (2015 Version)](https://www.miit.gov.cn/zwgk/zcwj/wjfb/tg/art/2020/art_e98406cd89844f7e92ea1bcf3b5301e0.html), enterprises that provide private line services in China must have both permits of [A26 domestic communication facilities services] and [A14 Internet data transmission business] issued by MIIT, or obtained relevant approval document. These enterprises should offer data transmission services within the business scope, and in the applicable geographic regions as stipulated in the approval document.

<span id ="69"></span>
- Why is a legitimate line access is necessary for Tencent Cloud?
According to the relevant national laws and regulations as well as the [Notice on Regulating the Internet Network Access Marketplace (MIIT [2017] No. 32)](https://www.miit.gov.cn/zwgk/zcwj/wjfb/txy/art/2020/art_7e2dbb4b014a43e98a76093cd96b450a.html), you should choose an eligible connection provider to complete the construction of private lines.

<span id ="70"></span>
- What are the consequences of using illegal private line service?
Using an illegal line may expose you to administrative penalty by the State regulatory authority and cause the line unavailability. In this case, Tencent Cloud accepts no responsibility.
