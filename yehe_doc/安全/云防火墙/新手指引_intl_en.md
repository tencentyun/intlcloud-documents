This topic helps you get started with Tencent Cloud Firewall (CFW).

## 1. Cloud Firewall basics
- [What features does Cloud Firewall offer?](https://intl.cloud.tencent.com/document/product/1160/49803)
- [What are the benefits of using Tencent Cloud Firewall?](https://intl.cloud.tencent.com/document/product/1160/49804)
- [What are some application scenarios of Cloud Firewall?](https://intl.cloud.tencent.com/document/product/1160/49805)
- [What are the common concepts of Cloud Firewall?](https://intl.cloud.tencent.com/document/product/1160/49806)

## 2. Billing modes of Cloud Firewall
Paid editions of Tencent Cloud Firewall include IPS Edition, Premium Edition, Enterprise Edition, and Ultimate Edition. To meet the needs of different customers with different asset scales, the editions differ in their feature modules and default specifications. Among them, the Premium Edition, Enterprise Edition, and Ultimate Edition support elastic scaling based on performance specifications and asset scale. For more information, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1160/49871).


## 3. Getting started
#### 3.1 Major features of Cloud Firewall
Tencent Cloud Firewall (CFW) is a SaaS firewall based on the public cloud environment that provides network perimeter protection and addresses security and management needs for unified access control and log audit. In addition to the features of traditional firewalls, CFW supports multi-tenancy and elastic scaling and is an essential network security infrastructure for cloud migration. For more information, please see [Overview](https://intl.cloud.tencent.com/document/product/1160/49803).
#### 3.2 Purchasing Cloud Firewall
Paid editions of Tencent Cloud Firewall include IPS Edition, Premium Edition, Enterprise Edition, and Ultimate Edition. You can purchase one of them on the [Purchase Cloud Firewall page](https://buy.cloud.tencent.com/cfw). For more information, please see [Purchase Method](https://intl.cloud.tencent.com/document/product/1160/49871).
#### 3.3 Using Cloud Firewall
After you purchase Cloud Firewall, you can use it in the following ways:
- Method 1: Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw) to perform operations. For more information, please see [Operation Guide](https://intl.cloud.tencent.com/document/product/1160/49809).
- Method 2: Use CFW with APIs. For more information, please see [API Documentation](https://www.tencentcloud.com/document/product/1160/51320).


## 4. Overview of console features

| If you want to | See |
|---------|---------|
| Configure firewall toggles for your public IPs and the associated cloud assets. | - |
|Manage traffic and protect assets in the private network, or forward network traffic based on SNAT and DNAT. |[NAT Firewall Toggle](https://intl.cloud.tencent.com/document/product/1160/49810)|
|Automatically detect VPC information and connections, and set a Cloud Firewall toggle for each pair of connected VPCs. |[Inter-VPC Firewall Toggle](https://intl.cloud.tencent.com/document/product/1160/49811)|
|View and manage the data and information of each asset in the Cloud Firewall console. |-|
|View and process security event alerts and blocked access. |[Alert Management](https://intl.cloud.tencent.com/document/product/1160/49837)|
|View the traffic access and bandwidth visually within a specified time frame. |[Traffic Monitoring](https://intl.cloud.tencent.com/document/product/1160/49822)|
|Filter domain names, or filter traffic by geographic location. |-|
|Use the security baseline feature for product security and stability.|-|
|Identify unknown risks beyond access control rules, monitor the north-south traffic of public IP addresses based on intrusion defense rules, and prevent CVM vulnerabilities from being exposed to the Internet. |[Intrusion Defense](https://intl.cloud.tencent.com/document/product/1160/49856)|
|View the Cloud Firewall logs.|[Log Audit](https://intl.cloud.tencent.com/document/product/1160/49861)|
|View the details of all the traffic logs stored in Cloud Firewall for the past 6 months based on account, retrieve and query logs with search statements, and use reporting and statistical analysis services. |[Log Analysis](https://intl.cloud.tencent.com/document/product/1160/49862)|
|Batch manage IP addresses with address templates. |[Address Template](https://intl.cloud.tencent.com/document/product/1160/49863)|


## 5. FAQs
- [What protocols does Cloud Firewall support?](https://intl.cloud.tencent.com/document/product/1160/49827)
- [What is peak bandwidth? Does it refer to uplink or downlink bandwidth?](https://intl.cloud.tencent.com/document/product/1160/49825#.E5.B3.B0.E5.80.BC.E5.B8.A6.E5.AE.BD.E6.98.AF.E6.8C.87.E4.BB.80.E4.B9.88.EF.BC.8C.E6.98.AF.E4.B8.8A.E8.A1.8C.E5.B8.A6.E5.AE.BD.E8.BF.98.E6.98.AF.E4.B8.8B.E8.A1.8C.E5.B8.A6.E5.AE.BD.EF.BC.9F)
- [Does it affect my business when the peak bandwidth is exceeded?](https://intl.cloud.tencent.com/document/product/1160/49825#question4)
- [How long are CFW logs stored by default? What is the maximum storage capacity?](https://intl.cloud.tencent.com/document/product/1160/49839#.E4.BA.91.E9.98.B2.E7.81.AB.E5.A2.99.E6.97.A5.E5.BF.97.E9.BB.98.E8.AE.A4.E5.AD.98.E5.82.A8.E5.A4.9A.E9.95.BF.E6.97.B6.E9.97.B4.EF.BC.9F.E6.9C.80.E5.A4.A7.E5.AD.98.E5.82.A8.E5.AE.B9.E9.87.8F.E6.98.AF.E5.A4.9A.E5.B0.91.EF.BC.9F)
- [What requests are blocked automatically in Block mode? Why do alerts still appear when Block mode is enabled?](https://intl.cloud.tencent.com/document/product/1160/49835#.E6.8B.A6.E6.88.AA.E6.A8.A1.E5.BC.8F.E4.B8.AD.EF.BC.8C.E4.BB.80.E4.B9.88.E6.83.85.E5.86.B5.E4.B8.8B.E4.BC.9A.E8.87.AA.E5.8A.A8.E6.8B.A6.E6.88.AA.EF.BC.9F.E4.B8.BA.E4.BB.80.E4.B9.88.E5.BC.80.E5.90.AF.E4.BA.86.E6.8B.A6.E6.88.AA.E6.A8.A1.E5.BC.8F.E8.BF.98.E4.BC.9A.E6.9C.89.E5.91.8A.E8.AD.A6.EF.BC.9F)
- [Why are requests from malicious IP addresses not blocked?](https://intl.cloud.tencent.com/document/product/1160/49835)
- [Is my business affected when I enable or disable Cloud Firewall, scale up, add CAM authorization, and enable or disable intrusion defense?](https://intl.cloud.tencent.com/document/product/1160/49842#.E4.BA.91.E9.98.B2.E7.81.AB.E5.A2.99.E7.9A.84.E5.BC.80.E5.85.B3.E3.80.81.E6.89.A9.E5.AE.B9.E3.80.81.E6.B7.BB.E5.8A.A0-cam-.E6.8E.88.E6.9D.83.E3.80.81.E5.85.A5.E4.BE.B5.E9.98.B2.E5.BE.A1.E5.BC.80.E5.85.B3.E6.98.AF.E5.90.A6.E4.BC.9A.E5.AF.B9.E4.B8.9A.E5.8A.A1.E9.80.A0.E6.88.90.E5.BD.B1.E5.93.8D.EF.BC.9F)
- [Can I modify the configurations for Cloud Firewall?](https://intl.cloud.tencent.com/document/product/1160/49841)
- [Can I renew my Cloud Firewall subscription when it expires? Will I lose all my resources when my subscription expires?](https://intl.cloud.tencent.com/document/product/1160/49841)


## 6. Feedback and suggestions
If you have any questions or suggestions when using Tencent Cloud Firewall, you can submit your feedback through the following channels. A dedicated person will contact you to solve your problems.
- If you have any feedback regarding CFW documentation, such as incorrect links, content, or APIs, please click **Send Feedback** on the right side of the documentation page, or select the target content.
- If you have any questions, please [contact us](https://intl.cloud.tencent.com/contact-us) or [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&step=1).
