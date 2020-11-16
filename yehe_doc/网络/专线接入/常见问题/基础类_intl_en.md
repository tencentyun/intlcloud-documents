**Basic Concept FAQs**

- [What is Direct Connect?](#01)
- [What does Direct Connect consist of?](#02)
- [How long does it take to apply for Direct Connect to Tencent Cloud?](#03)
- [Is Direct Connect supported outside Mainland China?](#05)
- [What are the limits for using Direct Connect?](#06)
- [Is the size of transferred data limited during use of Direct Connect??](#07)
- [What are the differences between Direct Connect and IPSec VPN Connection?](#08)
- [Can Direct Connect be used across accounts?](#51)
- [How do I configure alarms for Direct Connect?](#32)

**ISP FAQs**

- [What ISPs are supported by access points of Tencent Cloud Direct Connect?](#21)

**Connection FAQs**

- [Can I modify the parameters of a connection application submitted?](#11)
- [Can a connection access Tencent Cloud resources in multiple regions?](#12)
- [Why is the connection always in "applying" status?](#13)
- [How long will a connection take effect after it is approved?](#14)
- [What is the purpose of the bandwidth of a connection?](#15)
- [What is the “carrier circuit number” of a connection?](#16)
- [Can I change the address of a connection?](#17)
- [Can I deploy my own devices in a Tencent Cloud data center?](#18)

**Dedicated Tunnel FAQs**

- [Why is the dedicated tunnel always in "configuring" or "modifying" status?](#31)
- [Notice on the shared connection deactivation](#04)

**Compliance FAQs**

- [Why is the shared tunnel suspended?](#63)
- [Can I continue using the shared connection?](#67)
- [Why do I need to choose a legitimate private line service?](#68)
- [Why must I use a legitimate line to access Tencent Cloud?](#69)
- [What are the consequences of using an illegal private line?](#70)

<span id ="01"></span>

### What is Direct Connect?

[Direct Connect](https://intl.cloud.tencent.com/document/product/216/544) provides a secure and fast connection between Tencent Cloud and your on-premises IDC. You can connect Tencent Cloud computing resources in multiple regions with a single dedicated connection to implement flexible and reliable hybrid cloud deployment.

<span id ="02"></span>

### What does Direct Connect consist of?

Direct Connect consists of connections, dedicated tunnels, and Direct Connect gateways. For more information, see [Product Overview](https://intl.cloud.tencent.com/document/product/216/544).
<span id ="03"></span>

### How long does it take to apply for Direct Connect to Tencent Cloud?

You can apply for Direct Connect by doing as follows:

- **Build a connection**:
  - Lay fiber cable: this process is the **most time-consuming** construction. The laying period is subject to the connection provider's capability and connection conditions at both ends. The following is the general **reference values** of laying periods:
    - In Mainland China: 20 days for an intra-region connection and 30 days for a cross-region connection.
    - Outside Mainland China: the period varies widely by region; for example, it is 1 month for Hong Kong (China) and 1.5-2 months for regions in Europe and North America.
  - Apply for a connection by yourself: log in to the [Direct Connect Console](https://console.cloud.tencent.com/dc/dc) and enter the parameters as instructed in [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244). You need to confirm with your connection provider for some parameter settings such as port type and bandwidth.
    After your application is submitted, a Tencent Cloud Direct Connect delivery engineer will check with you the details of your needs and initiate the construction in three days. Generally, resources such as ports and modules can be prepared in one week after construction is initiated. Then, wait for the connection provider to lay the fiber cable.
  - Apply for a connection through a partner: as Tencent Cloud's Direct Connect partners have been interconnected with Tencent Cloud over NNI, purchasing a connection from one partner can eliminate the need for connection construction in Tencent Cloud. You can directly create a dedicated tunnel to share the partner's connection. Therefore, we recommend you purchase the connection from a Tencent Cloud partner.
- **Apply for a dedicated tunnel**: submit an application in the [Tencent Cloud Console](https://console.cloud.tencent.com/dc/dcConn) as instructed in [Applying for a Tunnel](https://intl.cloud.tencent.com/document/product/216/19250). After your application is submitted, the tunnel can be created in 10 minutes (if you share a partner’s connection, the tunnel can be created only after the application is approved by the partner).
- **Apply for a Direct Connect gateway and configure the route table**: they are both created automatically and immediately after you submit the application.

<span id ="51"></span>

### Can Direct Connect be used cross accounts?

Yes. The shared connection feature allows you to use a connection across accounts, but a new tunnel (including dedicated tunnels and Internet tunnels) no longer supports this feature since August 1, 2020 00:00:00.

- If you want to use the Direct Connect service, you can connect to Tencent Cloud by [applying for a tunnel](https://intl.cloud.tencent.com/document/product/216/19250). For more information about the connection methods, contact your Tencent Cloud rep.
- If you have used the shared connection and deleted a shared tunnel, the quota of the shared tunnel will be released. For example, you applied for a quota of 3 shared tunnels and bound them to a connection. After you deleting the shared tunnel 1, the quota for tunnels changes to 2.

  <span id ="11"></span>

### Can I modify the parameters of a connection application submitted?

You can modify the following parameters of the connection before the application is pushed by the Tencent Cloud Direct Connect delivery engineer to the backend for review: ISP, access point, port type, and connection type. If you no longer need this application, you can request the engineer to reject it, and you can submit a new one.

<span id ="21"></span>

### What ISPs are supported by access points of Tencent Cloud Direct Connect?

Most Tencent Cloud Direct Connect access points are deployed in data centers of neutral IDC ISPs and support access from any connection provider.
You can log in to the [Direct Connect Console](https://console.cloud.tencent.com/dc/dc), click **+New** to create a connection, and choose different ISPs, so you can view the Direct Connect access points supporting access from the selected ISP.

<span id ="22"></span>

### How can I locate a connection provider?

You can [submit a ticket](https://console.cloud.tencent.com/workorder/category), and a Tencent Cloud Direct Connect delivery engineer will recommend an optimal provider for you.

<span id ="12"></span>

### Can a connection access Tencent Cloud resources in multiple regions?

Yes. Access from one point to cloud resources in all regions is supported in two ways:

- Tencent Cloud Direct Connect access point devices support 802.1Q VLAN encapsulation. After the Trunk mode is enabled, a connection can support multiple VLANs, and you can use different VLANs to create different dedicated tunnels so as to access cloud VPC resources in multiple regions.
- You can also use [CCN](https://intl.cloud.tencent.com/product/ccn) to access cloud VPC resources in multiple regions.

<span id ="13"></span>

### Why is the connection always in "applying" status?

After you submit an application for a connection, a Tencent Cloud Direct Connect delivery engineer will check with you the details as soon as possible and initiate the corresponding review and construction processes. If your project is urgent, you can contact your delivery engineer or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to get the latest progress.

<span id ="14"></span>

### How long will a connection take effect after it is approved?

It will take effect in one month. If you fail to pay for the connection construction within one month, the connection environment may change, and the resources will be repossessed. If you still need a connection, you must submit a new application.

<span id ="15"></span>

### What is the purpose of the bandwidth of a connection?

The bandwidth of a connection is for record only and is not used to limit speed. If your connection speed changes, you can contact your Tencent Cloud Direct Connect delivery engineer or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to modify the bandwidth value in the console.

<span id ="16"></span>

### What is the "carrier circuit number" of a connection?

It is a unique circuit identifier provided by the connection provider. Please make sure that it is correct, as it is required when you locate a line with the connection provider during future line maintenance.

<span id ="17"></span>

### Can I change the address of a connection?

- If you want to change your local IDC address, please submit your change request to your connection provider.
- If you want to change the address of the access point in Tencent Cloud, please consult your Tencent Cloud Direct Connect delivery engineer.

<span id ="18"></span>

### Can I deploy my own devices in a Tencent Cloud data center?

No.

<span id ="31"></span>

### Why is the dedicated tunnel always in "configuring" or "modifying" status?

Generally, it takes several minutes to configure a new or modified dedicated tunnel. If the configuration is not completed in ten minutes, the configuration encountered a problem, and the backend engineer will fix it as soon as possible. You can also check the latest progress with your Tencent Cloud Direct Connect delivery engineer.


<span id ="04"></span>

### Notice on the shared connection deactivation

The shared connection feature allows you to use a connection across accounts, but a new tunnel (including dedicated tunnels and Internet tunnels) no longer supports this feature since August 1, 2020 00:00:00.

- If you want to use the Direct Connect service, you can connect to Tencent Cloud by [applying for a tunnel](https://intl.cloud.tencent.com/document/product/216/19250). For more information about the connection methods, contact your Tencent Cloud rep.
- If you have used the shared connection and deleted a shared tunnel, the quota of the shared tunnel will be released. For example, you applied for a quota of 3 shared tunnels and bound them to a connection. After you deleting the shared tunnel 1, the quota for tunnels changes to 2.

<span id ="05"></span>

### Is Direct Connect supported outside Mainland China?

Yes. Direct Connect is supported and can be applied for in all regions displayed at Tencent Cloud's official website. The corresponding LOA will be issued by Tencent Cloud. In regions outside Mainland China, Tencent Cloud can provide one-stop connection delivery services. For more information, consult your Direct Connect delivery engineer.

<span id ="06"></span>

### What are the limits for using Direct Connect?

Direct Connect resources and connections are limited. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/216/546).

<span id ="07"></span>

### Is the size of transferred data limited during use of Direct Connect?

No. You can transfer data in any size, and the highest speed is the selected connection bandwidth.
For other limits, see [Use Limits](https://intl.cloud.tencent.com/document/product/216/546).

<span id ="32"></span>

### How do I configure alarms for a connection?

Go to the Cloud Monitoring Console to [create a policy](https://console.cloud.tencent.com/monitor/policycreate). On the **Create Policy** page, select **Connection** or **Dedicated Tunnel** for the **Policy Type**, and complete other configurations of the alarm policy.

<span id ="08"></span>

### What are the differences between Direct Connect and IPSec VPN Connection?

- A VPN connection uses the public network and the IPsec protocol to establish an encrypted network connection between your IDC and VPC. You can purchase, validate, and configure a VPN gateway in just a few minutes. However, a VPN connection may be interrupted due to public network quality problems such as Internet jitters or congestion. If your business does not have a high requirement for the network connection quality, the VPN connection is a cost-effective choice for rapid deployment.
- By contrast, Direct Connect provides a dedicated network connection solution. Its construction takes a longer time, but it can provide high-quality and high-reliability network connection services. If your business has a high requirement for the network quality and security, you can choose Direct Connect for deployment.

For more information, see [Product Overview](https://intl.cloud.tencent.com/document/product/216/544).


<span id ="63"></span>
### Why is the shared tunnel feature deactivated?
According to the relevant national laws, regulations and the [Notice on Regulating the Internet Network Access Marketplace (MIIT [2017] No. 32)](http://www.scio.gov.cn/xwfbh/xwbfbh/wqfbh/35861/36970/xgzc36976/Document/1559330/1559330.htm), Tencent Cloud only makes available the shared tunnel to enterprises that have both permits of [A26 domestic communication facilities services] and [A14 Internet data transmission business] issued by MIIT, or obtained relevant approval document. If you are eligible, you can submit a ticket to enable this feature. The shared tunnel shall be used with a separate direct connect gateway.

<span id ="67"></span>
### Can I continue using the shared connection?
Yes. But if you delete the shared connection, you cannot apply for a new one after August 1, 2020 00:00:00.

<span id ="68"></span>
### Why do I need to choose a legitimate private line service?
As required by the national laws, regulations and MITT [Telecom Service Catalog (2015 Version)](http://www.miit.gov.cn/n1146295/n1652858/n1652930/n4509627/c4564595/content.html), enterprises that provide private line services in China must have both permits of [A26 domestic communication facilities services] and [A14 Internet data transmission business] issued by MIIT, or obtained relevant approval document. These enterprises should develop data transmission services within the business scope, and in the applicable geographic regions as stipulated in the approval document.

<span id ="69"></span>
### Why must I use a legitimate line to access Tencent Cloud?
According to the relevant national laws and regulations as well as the [Notice on Regulating the Internet Network Access Marketplace (MIIT [2017] No. 32)](http://www.scio.gov.cn/xwfbh/xwbfbh/wqfbh/35861/36970/xgzc36976/Document/1559330/1559330.htm), you should choose a qualified connection provider to complete the construction of private lines.

<span id ="70"></span>
### What are the consequences of using an illegal private line?
Using an illegal line may expose you to administrative punishment of the state regulatory authority, cause the line unavailability, and make you fully liable. Tencent Cloud accepts no responsibility.
