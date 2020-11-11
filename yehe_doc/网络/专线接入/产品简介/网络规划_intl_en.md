Read this document to learn about the connection planning before  building a network architecture for Direct Connect.

## Background
A connection planning improves the stability and high availability of the network architecture for Direct Connect, and minimizes the impact from failures including device, port/fiber optic component, connection and data center at the access point. See the table below for the description and cause of failures.
<table>
<tr>
<th width="20%">Failure</th>
<th width="40%">Description</th>
<th width="40%">Cause</th>
</tr>
<tr>
<td>Connection</td>
<td>The connection communication fails or many packets are discarded.</td>
<td>The connection is damaged. For example, the cable is cut off.</td>
</tr>
<tr>
<td>Port/fiber optic component</td>
<td>The port/fiber optic component fails to be read or has an transfer exception due to hardware or software failures.</td>
<td><ul><li>Hardware failure: incompatible version, contaminated or damaged port.</li><li>Software failure: incorrect port status, port in **UP** status without receiving or sending packets, frequent port on/off, or cyclic redundancy check (CRC) error.</li></ul></td>
</tr>
<tr>
<td>Network device</td>
<td>The exchange or router on the IDC side is unavailable.</td>
<td><ul><li>Hardware failure: power supply, port, component or cable failures.</li><li>Software failure: exchange/router error or incorrectly configured.</li></ul></td>
</tr>
<tr>
<td>Data center at the access point</td>
<td>The data center encounters network disconnection, or the access point is unavailable.</td>
<td>The data center cannot function normally due to earthquakes, fires or other disasters.</td>
</tr>
</table>

<span id="planning"></span>
## Planning Ideas
<span id="capacity"></span>
### Capacity panning
The capacity planning is designed to meet business bandwidth requirements at a reasonable cost and guarantee the business operation in the event of a connection failure. To achieve this, you can:
- Apply for connections twice your actual needs.
- Maintain the connection utilization (current peak bandwidth/connection bandwidth * 100%) 50% or less.

Assume your business needs 3 Mpbs of bandwidth, you can apply for two connections with 5 Mpbs of bandwidth to each Tencent Cloud access point, each connection will be used about 30%. If one connection faults, the business traffic will quickly switch to the standby connection to ensure the business continuity. After the switchover, the standby connection will be used about 60%. In this way, only the connection load temporarily increases, and the business data is unaffected.
![](https://main.qcloudimg.com/raw/ab7ec6d0a10c4ec54a4797b7cd063fe5.png)

### Expansion planning
The expansion planning is designed to meet the surging business demand at a reasonable cost. Depending on the expansion cycle, you need to plan differently as follows:
- If you need an urgent expansion, you can apply for a connection based on the estimated business bandwidth, so that you can adjust the bandwidth limit to maintain your business when the traffic surges.
- If you don’t need an expansion in the near future, you can apply for a new connection based on your actual expansion needs. The expansion will take 2-3 months.
>? A single expansion exceeding 100 Gbps of bandwidth requires a longer period. Please develop an expansion plan in advance for high-bandwidth businesses.


### Disaster recovery planning
The disaster recovery is designed to improve the high availability of a network architecture and minimize the failure (including port/fiber optic component, network device, and data center at the access point) impact on business operations.
To avoid single points of failures, we recommend that you develop a disaster recovery plan for access points, physical lines, and hardware devices.
- Access point: the local IDC uses connections of different physical lines to two intra-region Tencent Cloud access points.
- Physical line: different physical lines provided by carriers are used to connect to a Tencent Cloud access point.
- Hardware devices: both network devices and fiber optic components have redundant backups.

Assume you connect your local IDC to two intra-region Tencent Cloud access points according to [capacity planning (#capacity) requirements, as shown in the figure below. If the connection to access point A is disconnected due to port/fiber optic component, network devices or data center failures, the business traffic will quickly switch to the connection to access point B, without losing business data or interrupting businesses.
![](https://main.qcloudimg.com/raw/799029a7a0e60219e702d19678251493.png)

## Sample Architectures
Tencent Cloud provides the following four network architectures for Direct Connect to facilitate your network planning.
<table>
<tr>
<th width="20%">Architecture</th>
<th width="55%">Use Case</th>
<th width="5%">Business Elasticity</th>
<th width="5%">Availability</th>
<th width="5%">Cost</th>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/216/38527#.E5.9B.9B.E7.BA.BF.E5.8F.8C.E6.8E.A5.E5.85.A5.E7.82.B9.E6.A8.A1.E5.BC.8F.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89" target="_blank">Four connections to two access points (recommended)</a></td>
<td>Suitable for use cases that require excellent business availability and elasticity, including the key production and real-time data transaction.</td>
<td>Highest</td>
<td>Highest</td>
<td>Highest</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/216/38527#.E5.8F.8C.E7.BA.BF.E5.8F.8C.E6.8E.A5.E5.85.A5.E7.82.B9.E6.A8.A1.E5.BC.8F.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89" target="_blank">Two connections to two access points (recommended)</a></td>
<td>Suitable for key business that requires high availability and elasticity.</td>
<td>Medium</td>
<td>Higher</td>
<td>Medium</td>
</tr>
<tr>
<td>
<a href="https://intl.cloud.tencent.com/document/product/216/38527#.E5.8F.8C.E7.BA.BF.E5.8D.95.E6.8E.A5.E5.85.A5.E7.82.B9.E6.A8.A1.E5.BC.8F" target="_blank">Two connections to one access point</a></td>
<td>Suitable for non-critical business, including the cloud development and testing environments.</td>
<td>Medium</td>
<td>Medium</td>
<td>Medium</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/216/38527#.E5.8D.95.E7.BA.BF.E5.8D.95.E6.8E.A5.E5.85.A5.E7.82.B9.E6.A8.A1.E5.BC.8F" target="_blank">Connection to one access point</a></td>
<td>Suitable for non-critical business that does not require high elasticity and availability.</td>
<td>Low</td>
<td>Low</td>
<td>Low</td>
</tr>
</table>

## Four Connections to Two Access Points (Recommended)
### Overview
- **Description**: this architecture connects your IDC to two intra-region Tencent Cloud access points using primary and secondary connections respectively, and then accesses Tencent Cloud VPCs.
- **Use cases**: suitable for use cases that require excellent business availability and elasticity, including the key production and real-time data transaction.
- **Cost**: high.
![](https://main.qcloudimg.com/raw/37caeac1cdcbaf0ab63227ad32fedbb1.png)

### Disaster recovery
The following table describes the impact of this network architecture on business under various failures when the [planning ideas](#planning) are met.
<table>
<tr>
<th>Failure</th>
<th>Business Impact</th>
</tr>
<tr>
<td>Connection</td>
<td>The connections loads increase, and the business continues.</td>
</tr>
<tr>
<td>Port/fiber optic component</td>
<td>The connections loads increase, and the business continues.</td>
</tr>
<tr>
<td>Network device</td>
<td>The connections loads increase, and the business continues.</td>
</tr>
<tr>
<td>Data center at the access point</td>
<td>The connections loads increase, and the business continues.</td>
</tr>
</table>

## Two Connections to Two Access Points (Recommended)
### Overview
- **Description**: this architecture connects your IDC to two intra-region Tencent Cloud access points using one connection respectively, and then accesses Tencent Cloud VPCs.
- **Use cases**: suitable for key business that requires high availability and elasticity.
- **Cost**: medium.
![](https://main.qcloudimg.com/raw/95426eded21b41c357936861d63ba8c1.png)

### Disaster recovery
The following table describes the impact of this network architecture on businesses under various failures.
<table>
<tr>
<th width="18%">Failure</th>
<th width="52%">Business Impact</th>
<th width="30%">Recovery Measures</th>
</tr>
<tr>
<td>Connection</td>
<td><ul><li>If each connection is used 50% or less, the connection loads burst and the business continues.</li><li>If each connection is used greater than 50%, the connection will be full-loaded, some data will be lost, and the business continues.</li></ul>
</td>
<td>If the business data is lost, you need to apply for a new connection and spend 2-3 months to restore the business.</td>
</tr>
<tr>
<td>Network device</td>
<td>
<ul><li>If each connection is used 50% or less, the connection loads burst and the business continues.</li><li>If each connection is used greater than 50%, the connection will be full-loaded, some data will be lost, and the business continues.</li></ul>
</td>
<td>If business data is lost, you need to check and repair the network devices. The recovery time depends on the specific failure.</td>
</tr>
<tr>
<td>Port/fiber optic component</td>
<td>
<ul><li>If each connection is used 50% or less, the connection loads burst and the business continues.</li><li>If each connection is used greater than 50%, the connection will be full-loaded, some data will be lost, and the business continues.</li></ul>
</td>
<td>If business data is lost, you need to check and repair the ports or fiber optic components. The recovery time depends on the specific failure.</td>
</tr>
<tr>
<td>Data center at the access point</td>
<td>
<ul><li>If each connection is used 50% or less, the connection loads burst and the business continues.</li><li>If each connection is used greater than 50%, the connection will be full-loaded, some data will be lost, and the business continues.</li></ul>
</td>
<td>If business data is lost, you can:<ul><li>Contact the data center carrier to repair the failure. The recovery time depends on the specific failure.</li><li>Reapply connections to other access points. The recovery takes about 2-3 months.</li></ul></td>
</tr>
</table>

## Two Connections to One Access Point

### Overview
- **Description**: this architecture connects your IDC to one Tencent Cloud access point using two connections, and then accesses Tencent Cloud VPCs.
- **Use cases**: suitable for non-critical business, such as cloud development and testing environments.
- **Cost**: medium.
![](https://main.qcloudimg.com/raw/c69786418c3d7359d57a457f471bebee.png)

### Disaster recovery
The following table describes the impact of this network architecture on businesses under various failures.
<table>
<tr>
<th width="20%">Failure</th>
<th width="40%">Business Impact</th>
<th width="40%">Recovery Measures</th>
</tr>
<tr>
<td>Connection</td>
<ul><li>If each connection is used 50% or less, the connection loads burst and the business continues.</li><li>If each connection is used greater than 50%, the connection will be full-loaded, some data will be lost, and the business continues.</li></ul>
<td>If the business data is lost, you need to apply for a new connection and spend 2-3 months to restore the business.</td>
</tr>
<tr>
<td>Network device</td>
<td>The business will be interrupted.</td>
<td>You need to troubleshoot and repair the faulty network devices. The recovery time depends on the specific failure.</td>
</tr>
<tr>
<td>Port/fiber optic module</td>
<td>The business will be interrupted.</td>
<td>You need to troubleshoot and repair the faulty local ports or fiber optic components. The recovery time depends on the specific failure.</td>
</tr>
<tr>
<td>Data center at the access point</td>
<td>The business will be interrupted.</td>
<td><ul><li>Contact the data center carrier to fix the failure. The recovery time depends on the specific failure.</li><li>Reapply connections to other access points. The recovery takes about 2-3 months.</li></ul></td>
</tr>
</table>

## A Connection to One Access Point

### Overview
- **Description**: this architecture connects your IDC to one Tencent Cloud access point using a connection, and then accesses Tencent Cloud VPCs.
- **Use cases**: suitable for non-critical business that does not require high elasticity and availability.
- **Cost**: medium.
![](https://main.qcloudimg.com/raw/2623e871b9ec8af7fc77973abde88eab.png)

### Disaster recovery
The following table describes the impact of this network architecture on businesses under various failures.
<table>
<tr>
<th width="20%">Failure</th>
<th width="20%">Business Impact</th>
<th width="60%">Recovery Measures</th>
</tr>
<tr>
<td>Connection</td>
<td>The business will be interrupted.</td>
<td>Reapply for a connection. The recovery takes about 2-3 months.</td>
</tr>
<tr>
<td>Network device</td>
<td>The business will be interrupted.</td>
<td>You need to troubleshoot and repair the faulty network devices. The recovery time depends on the specific failure.</td>
</tr>
<tr>
<td>Port/fiber optic module</td>
<td>The business will be interrupted.</td>
<td>You need to troubleshoot and repair the faulty local ports or fiber optic components. The recovery time depends on the specific failure.</td>
</tr>
<tr>
<td>Data center at the access point</td>
<td>The business will be interrupted.</td>
<td><ul><li>Contact the data center ISP to fix the failure. The recovery time depends on the specific failure.</li><li>Reapply connections to other access points. The recovery takes about 2-3 months.</li></ul></td>
</tr>
</table>
