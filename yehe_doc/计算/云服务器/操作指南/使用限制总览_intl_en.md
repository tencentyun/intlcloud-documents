## Account Prerequisites for Purchasing CVM Instances

- You need to sign up for a Tencent Cloud account. For registration instructions, see [Sign Up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).
- You need to verify your identity. For more information, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).
- When you create a pay-as-you-go CVM, the system will freeze the cost of one hardware bill cycle. Make sure your account has sufficient balance to pay for the order.

## Use Limits for CVM Instances

- Virtualized software cannot be installed or re-virtualized (such as installing VMware or Hyper-V).
- You cannot use sound cards or mount external hardware devices (such as ISO file, USB drive, external disk and U-key).
- The public gateway is available only in Linux systems.

## Purchase Limits for CVM Instances

- For each user, the **quota** of pay-as-you-go CVM instances in each availability zone is 30.
- For more information, see [CVM Instance Purchase Limits](https://intl.cloud.tencent.com/document/product/213/2664).


## Image Limits

- Public images: no use limits.
- Custom image: each region supports a maximum of 10 custom images.
- Shared image: each custom image can be shared with a maximum of 50 Tencent Cloud users, and only be shared with accounts in the same region as the source account.
For more information, see [Image Types](https://intl.cloud.tencent.com/document/product/213/4941).

## Limits on Elastic Public IP Addresses (EIPs)

#### Limits

| Resources | Limit |
|---------|:---------:|
| Number of EIPs for each Tencent Cloud account in each region | 20 |
| Number of daily purchase applications of each Tencent Cloud account in each region | Quota \*2 times |
| Number of times public IPs can be reassigned to each account for free per day when an EIP is unbound | 10 times |

#### Limits on public IP addresses bound to a CVM

Starting from September 18, 2019 (inclusive), the maximum number of public network IP addresses that can be bound to a CVM instance has been changed based on its CPU configuration, as shown in the table below.
> This limit does not apply to CVM instances purchased before 00:00 on September 18, 2019. For these instances, the number of public IP addresses bound to each instance is equal to the [number of private IP addresses](https://intl.cloud.tencent.com/document/product/576/18527) supported by your server.
>

| Number of CPUs on a CVM | Maximum Number of Public IP Addresses Can Be Bound (Including Common Public IP Addresses and EIPs) |
|---------|---------|
| CPU: 1 - 5 | 2 |
| CPU: 6 - 11 | 3 |
| CPU: 12 - 17 | 4 |
| CPU: 18 - 23 | 5 |
| CPU: 24 - 29 | 6 |
| CPU: 30 - 35 | 7 |
| CPU: 36 - 41 | 8 |
| CPU: 42 - 47 | 9 |
| CPU: ≥ 48 | 10 |

## ENI Limits

Based on CPU and memory configurations, the number of ENIs that can be bound to a CVM differs from the number of private IPs that can be bound to an ENI. The limits are shown in the following table:
> The number of IPs bound to a single ENI only represents the maximum number of IPs can be bound to an ENI. EIP quota is not based on this upper limit, but EIP [use limits](https://intl.cloud.tencent.com/document/product/213/5733).

| CVM Configuration | Number of EIPs | Number of Private IP Addresses Bound to a Single ENI |
| ------------------- | :---- | :------ |
| CPU: 1 core </br>Memory: 1 GB | 2 | 2 |
| CPU: 1 core </br>Memory: > 1 GB | 2 | 6 |
| CPU: 2 cores | 2 | 10 |
| CPU: 4 cores </br>Memory: < 16 GB | 4 | 10 |
| CPU: 4 cores </br>Memory: > 16 GB | 4 | 20 |
| CPU: 8 - 12 cores: | 6 | 20 |
| CPU: >12 cores | 8 | 30 |


## Bandwidth Limits

- Maximum outbound bandwidth (downstream bandwidth)
<table>
    <tr>
       <th rowspan="2"><b>Network Billing Method</b></th> 
       <th colspan="2" ><b>Instance</b></th>
       <th rowspan="2"><b>Maximum Bandwidth(Mbps)</b></th>	
   </tr>
    <tr>
       <th><b>Instance Billing Method</b></th> 
       <th><b>Instance Configuration</b></th> 
    </tr>
	<tr>
	      <td>Bill-by-traffic</td> 
        <td >Pay-as-you-go Instance</td> 
        <td >ALL</td> 
				<td>0 - 100</td>    
   </tr>
	 <tr>
		    <td>Bill-by-bandwidth</td> 
        <td >Pay-as-you-go Instance</td> 
        <td >ALL</td> 
				<td>0 - 100</td>      
   </tr>
    <tr>
		    <td>Shared Bandwidth</td> 
        <td colspan="2">ALL</td> 
        <td>0 - 200 or no speed limit</td>    
    </tr>
</table>

- Maximum inbound bandwidth (upstream bandwidth)
	- If the fixed bandwidth you purchased is larger than 10 Mbps, the public network inbound bandwidth distributed by Tencent Cloud will be equal to the purchased bandwidth.
	- If the fixed bandwidth you purchased is less than 10 Mbps, Tencent Cloud will distribute 10 Mbps public network inbound bandwidth.

## Disk Limits

<table>
	<tr><th>Limit Type</th><th>Description</th></tr>
	<tr><td>Elastic cloud disk capability</td><td>Starting from May 2018, all data disks purchased with CVMs are elastic cloud disks, which support unmounting and remounting on CVMs. This feature is supported in all <a href="https://intl.cloud.tencent.com/document/product/213/35071">availability zones</a>.</td></tr>
	<tr><td>Cloud disk performance</td><td>I/O performance takes effect concurrently.</br>For example, a 1-TB SSD has a maximum random IOPS of 26,000, meaning its IOPS for both reads and writes can reach this value. Due to performance limits, if the block size in this example is 4 KB or 8 KB, the IOPS can reach the maximum. If the block size is 16 KB, the IOPS cannot reach the maximum (because throughput has reached the limit of 260 MB/s.)</td></tr>
	<tr><td>Number of elastic cloud disks that can be mounted to a CVM</td><td>A maximum of 20.</td></tr>
	<tr><td>Number of snapshots in one region</td><td>64 + number of disks in the region * 64.</td></tr>
	<tr><td>Mounting cloud disks to CVM</td><td>The instance and cloud disks must be in the same availability zone.</td></tr>
	<tr><td>Snapshot rollback</td><td>Snapshot data can only be rolled back to the cloud disk where the snapshot was created.</td></tr>
	<tr><td>Type of cloud disks used to create snapshots</td><td>Only snapshots of data disks can be used to create new elastic cloud disks.</td></tr>
	<tr><td>Size of cloud disks used to create snapshots</td><td>The size of new cloud disks created from snapshots must be larger than or equal to that of the source cloud disks.</td></tr>
</table>


## Security Group Limits

- Security groups are divided by region. The CVM can only be bound to security groups in the same region.
- Security groups are applicable to CVM instances in any [network environment](https://intl.cloud.tencent.com/document/product/213/5227).
- Each user can set a maximum of 50 security groups for each project in a region.
- A maximum of 100 inbound or outbound rules can be set for a security group.
- One CVM can have multiple security groups, and one security group can be associated with multiple CVMs.
- Security groups associated with CVMs in **basic network** **cannot filter** packets from or towards TencentDB and elastic cache (Redis and Memcached). You can use iptables to filter traffic for such instances.
- The limits are as follows:
<table>
<tr><th>Item</th><th>Limit</th></tr>
<tr><td>Number of security group</td><td>50 per region</td></tr>
<tr><td>Number of rules for a security group</td><td>100 (Inbound/Outbound)</td></tr>
<tr><td>Number of instances associated with a security group</td><td>100</td></tr>
<tr><td>Number of security groups associated with an instance</td><td>5</td></tr>
<tr><td>Number of rules that reference security group ID for each security group</td><td>10</td></tr>
</table>

## VPC Limits

| Resource | Limit |
|---------|---------|
| Number of VPC instances per region for each account | 5 |
| Number of subnets per VPC instance | 10 |
| Number of basic network CVMs can be associated per VPC | 100 |
| Number of route tables per VPC | 10 |
| Number of routing tables associated with the subnet | 1 |
| Number of routing policies per route table | 100 |
| Number of default HAVIP per PVC | 10 |

