## Account limits for purchasing CVM instances

- You need to sign up for a Tencent Cloud account. For more information on registration, see [Sign Up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).
- You need to verify your identity. For more information, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).
- If you create a pay-as-you-go CVM, the system will freeze the cost of one-hour CVM usage. Make sure that your account has sufficient balance for the order.

## CVM instance use limits

- Virtualized software cannot be installed or re-virtualized (such as installing VMware or Hyper-V).
- You cannot use sound cards or mount external hardware devices (such as USB flash drives, external disks, and U-keys).
- The public gateway is available only in Linux operating system.

## CVM instance purchase limits

- For each user, the **quota** of pay-as-you-go CVM instances in each availability zone is 30.
- For more information, see [CVM Instance Purchase Limits](https://cloud.tencent.com/document/product/213/2664).


## Image Limits

- Public images: no use limits.
- Custom images: each region supports a maximum of 10 custom images.
- Shared images: each custom image can be shared with a maximum of 50 Tencent Cloud users, and only be shared with accounts in the same region as the source account.
- For more information, see [Image Types Overview](https://intl.cloud.tencent.com/document/product/213/4941).

## EIP Limits

#### Quota limits

| Resource | Limit |
|---------|:---------:|
| Number of EIPs for each Tencent Cloud account in each region | 20 |
| Number of daily purchase applications for each Tencent Cloud account in each region | Quota \* 2 |
| Number of times that public IP addresses can be reassigned to each account for free per day when an EIP is unbound | 10 |

#### Limits on public IPs bound to a CVM

Starting September 18, 2019, the maximum number of public IPs can be bound to a single CVM had changed based on CPU configuration. The quotas are as shown below:
> This limit does not apply to CVM instances purchased before 00:00, September 18, 2019. For these instances, the number of public IPs can be bound to each instance is equal to the [number of private IPs](https://intl.cloud.tencent.com/document/product/576/18527) supported by your server.
>

| Number of CPUs on a CVM | Maximum number of public IPs can be bound (including public and elastic IPs) |
|---------|---------|
| 1–5 | 2 |
| 6–11 | 3 |
| 12–17 | 4 |
| 18–23 | 5 |
| 24–29 | 6 |
| 30–35 | 7 |
| 36–41 | 8 |
| 42–47 | 9 |
| ≥ 48 | 10 |

## ENI Limits

Based on CPU and memory configurations, the number of ENIs can be bound to a CVM differs from the number of private IPs can be bound to an ENI. The quotes are as shown below:
> The number of IP addresses bound to a single ENI indicates the maximum number allowed. The EIP quota is not provided based on this upper limit but based on EIP [use limits](https://intl.cloud.tencent.com/document/product/213/5733).

| CVM configuration | Number of ENIs | Number of private IPs bound to a single ENI |
| ------------------- | :---- | :------ |
| CPU: 1 core </br>Memory: 1 GB | 2 | 2 |
| CPU: 1 core </br>Memory: > 1 GB | 2 | 6 |
| CPU: 2 cores | 2 | 10 |
| CPU: 4 cores </br>Memory: < 16 GB | 4 | 10 |
| CPU: 4 cores </br>Memory: > 16 GB | 4 | 20 |
| CPU: 8–12 cores | 6 | 20 |
| CPU: > 12 cores | 8 | 30 |


## Bandwidth Limits

- Maximum outbound bandwidth (downstream bandwidth)
 - For CVMs created before 00:00, February 24, 2020, the following rules apply: 
<table>
<tr><th rowspan="2">Network Billing Method</th><th colspan="2">Instance</th><th rowspan="2">Maximum Bandwidth Range (Mbps)</th></tr>
<tr><th>Instance Billing Method</th><th>Instance Configuration</th></tr>
<tr><td>Bill-by-traffic</td><td>Pay-as-you-go instances</td><td>All</td><td>0–100</td></tr>
<tr><td>Bill-by-bandwidth</td><td>Pay-as-you-go instances</td><td>All</td><td>0–100</td></tr>
<tr><td>Bandwidth package</td><td colspan="2">All</td><td>0–2000</td></tr>
</table>

 - For CVMs created after 00:00, February 24, 2020, the following rules apply:
<table>
<tr><th rowspan="2">Network Billing Method</th><th colspan="2">Instance</th><th rowspan="2">Maximum Bandwidth Range (Mbps)</th></tr>
<tr><th style="width: 18.5607%;">Instance Billing Method</th><th style="width: 24.5814%;">Instance Configuration</th></tr>
<tr><td>Bill-by-traffic</td><td>Pay-as-you-go instances</td><td>All</td><td>0–100</td></tr>
<tr><td>Bill-by-bandwidth</td><td>Pay-as-you-go instances</td><td>All</td><td>0–100</td></tr>
<tr><td>Bandwidth package</td><td colspan="2">All</td><td>0–2000</td></tr>
</table>

- Maximum inbound bandwidth (upstream bandwidth)
	- If the fixed bandwidth you purchased is greater than 10 Mbps, Tencent Cloud will assign a public network inbound bandwidth equals to the purchased bandwidth.
	- If the fixed bandwidth you purchased is less than 10 Mbps, Tencent Cloud will assign 10-Mbps public network inbound bandwidth.

## Disk Limits

<table>
	<tr><th>Limit Type</th><th>Description</th></tr>
	<tr><td>Elastic cloud disk capability</td><td>Starting from May 2018, all data disks purchased with CVMs are elastic cloud disks, which can be unmounted from and remounted to CVMs. This feature is supported in all <a href="https://intl.cloud.tencent.com/document/product/213/35071">availability zones</a>.</td></tr>
	<tr><td>Elastic cloud disk performance</td><td>I/O performance takes effect concurrently.<br/>For example, if a 1-TB SSD has a maximum random IOPS of 26,000, its IOPS for both reads and writes can reach this value. Due to performance limits, if the block size in this example is 4 KB or 8 KB, the maximum IOPS can be reached. If the block size is 16 KB, the maximum IOPS cannot be reached (throughput has already reached the limit of 260 MB/s.)</td></tr>
	<tr><td>Number of elastic cloud disks mounted to a CVM</td><td>A maximum of 20</td></tr>
	<tr><td>Number of snapshots in one region</td><td>64 + Number of cloud disks in the region x 64</td></tr>
	<tr><td>Cloud disks mounted to a CVM</td><td>The CVM and cloud disks must be in the same availability zone.</td></tr>
	<tr><td>Snapshot rollback</td><td>Snapshot data can only be rolled back to the cloud disk where the snapshot was created.</td></tr>
	<tr><td>Type of cloud disks can be created using snapshots</td><td>Only snapshots of data disks can be used to create new elastic cloud disks.</td></tr>
	<tr><td>Size of cloud disks created using snapshots</td><td>The size of cloud disks created using snapshots must be larger than or equal to that of the source cloud disk.</td></tr>
</table>


## Security Group Limits

- Security groups are region-specific. A CVM can only be bound to security groups in the same region.
- Security groups are applicable to CVM instances in any [network environment](https://intl.cloud.tencent.com/document/product/213/5227).
- Each user can configure a maximum of 50 security groups for each project in a region.
- A maximum of 100 inbound or outbound rules can be configured for a security group.
- One CVM can have multiple security groups, and one security group can be associated with multiple CVMs.
- Security groups associated with CVMs on the **basic network** **cannot filter** packets from or to TencentDB and the elastic cache (Redis or Memcached). Instead, you can use iptables to filter traffic for such instances.
- The quotas are as shown below:
<table>
<tr><th>Item</th><th>Limit</th></tr>
<tr><td>Number of security groups</td><td>50 per region</td></tr>
<tr><td>Number of rules in a security group</td><td>100 for inbound rules and 100 for outbound rules</td></tr>
<tr><td>Number of CVM instances associated with a security group</td><td>2,000</td></tr>
<tr><td>Number of security groups associated with a CVM instance</td><td>5</td></tr>
<tr><td>Number of rules in each security group that reference the security group ID</td><td>10</td></tr>
</table>

## VPC Limits

| Resource | Limit |
|---------|---------|
| Number of VPC instances per region for each account | 5 |
| Number of subnets per VPC | 10 |
| Number of basic network CVMs can be associated with each VPC instance | 100 |
| Number of route tables per VPC | 10 |
| Number of route tables associated with each subnet | 1 |
| Number of routing policies per route table | 100 |
| Number of default HAVIPs per VPC | 10 |

