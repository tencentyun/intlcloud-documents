## Introduction
A peering connection is a high-bandwidth and high-quality cloud resources interconnection service that enables communication between resources on Tencent Cloud. Peering connections can be used across multiple regions, multiple accounts, and multiple types of heterogeneous networks, which can easily implement complex cloud scenarios, such as 2-region-3-DC and one server shared by game players. Peering connections enable interconnection between VPCs and between VPCs and BM networks, allowing you to deploy different businesses.
>!
>- Cross-region connectivity includes: cross-region connectivity between VPCs (cross-region peering connection) and cross-region Classiclink. To enable cross-region Classiclink, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC).
>- SLA assurance is provided for peering connection services. If the services do not meet the SLA criteria, you can apply for compensation according to the [SLA for peering connections](https://cloud.tencent.com/document/product/215/17800). 
>- When creating a cross-region peering connection, you must comply with the [cross-region interconnection service agreement](https://cloud.tencent.com/document/product/215/7682). If you violate the agreement, Tencent Cloud may restrict, suspend, or terminate your services under the agreement at any time as appropriate and retain the right to take legal action against you.

A VPC peering connection is a cross-VPC network interconnection service used for synchronizing office data. It enables interconnection between two VPCs as if they were on the same network. After routing policies are configured at both ends, interconnection is enabled between VPCs of the same user or different users in the same region or across regions. A peering connection does not depend on any separate hardware. Therefore, no single points of failure and bandwidth bottlenecks will occur in a peering connection.

## Product advantages
Peering connections have the following advantages over transmission on Internet.
- **Higher quality** 
Using the same in-house internal network as Tencent Group's businesses, the peering connections are not affected by the quality of Internet. Therefore, the peering connections provide significantly better availability, latency, and packet loss rate.
- **Higher security** 
 - The peering connections are protected by Tencent [Anti-DDoS](https://cloud.tencent.com/document/product/297) system, which is of high security.
 - The peering connections do not pass through wide area networks or ISP linkage. Therefore, they do not face the risk that packets are intercepted during transmission on Internet.
- **Lower cost**
The peering connection services are classified into platinum, gold, and silver levels. You can deploy the services differently based on your business requirements, which can reduce your costs.
 - Platinum: suitable for businesses that are the most sensitive to the communication quality, such as payment and game acceleration.
 - Gold: suitable for businesses that require transmission of key business data, such as transmission of enterprise business data and ERP.
 - Silver: suitable for businesses that are cost-sensitive and jitter-insensitive and have high requirements for security, such as remote data backup.

>!The application scenarios of platinum, gold, and silver services are as follows:
>- Gold: applicable to all regions. 
>- Platinum and silver: billed by monthly 95th percentile and applicable to some lines (Beijing, Shanghai, Guangzhou, Korea, and Hong Kong (China)). The services are currently in internal beta phase. If you need such services, please [submit a ticket](https://console.cloud.tencent.com/workorder).
