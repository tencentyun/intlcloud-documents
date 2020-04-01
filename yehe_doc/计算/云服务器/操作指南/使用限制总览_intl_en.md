## Account prerequisites for purchasing CVM instances

- You need to sign up for a Tencent Cloud account. For registration instructions, please see [Sign Up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).
- You need to verify your identity. For more information, please see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).
- When you create a pay-as-you-go CVM, the system will freeze the cost of one hardware bill cycle. Make sure your account has sufficient balance to pay for the order.

## Use limits for CVM instances

- Virtualized software cannot be installed or re-virtualized (such as installing VMware or Hyper-V).
- You cannot use sound cards or mount external hardware devices (such as ISO file, USB drive, external disk and U-key).
- The public gateway is available only in Linux systems.

## Purchase limits for CVM instances

- For each user, the **quota** of pay-as-you-go CVM instances in each availability zone is 30.
- For more information, please see [CVM Instance Purchase Limit](https://intl.cloud.tencent.com/document/product/213/2664?from_cn_redirect=1).


## Image Limits

- There is no limit on public images.
- Custom image: Each region supports a maximum of 10 custom images.
- Shared image: Each custom image can be shared with a maximum of 50 Tencent Cloud users, and only be shared with accounts in the same region as the source account.
For more information, please see [Image Types](https://intl.cloud.tencent.com/document/product/213/4941?from_cn_redirect=1).

## Elastic public IP limits

#### Limits

| Resources             | Limit          |
|---------|:---------:|
| Number of elastic public IPs for each Tencent Cloud account in each region | 20 |
| Number of daily purchase applications of each Tencent Cloud account in each region | Quota \* 2 times |
| Number of times public IPs can be reassigned to each account for free per day when an EIP is unbound | 10 times |

#### Limits on public IPs bound to CVM

Starting on September 18, 2019 (inclusive), the maximum number of public network IPs can be bound to a single CVM had changed based on its CPU configuration, as shown in the following table:
> This limit does not apply to CVMs purchased before 0:00 on September 18.
>
| Number of CPU on a CVM| Maximum number of public IPs can be bound (including common public IPs and elastic public IPs) |
|---------|---------|
| CPU：1 - 5 | 2 |
| CPU：6 - 11 | 3 |
| CPU：12 - 17 | 4 |
| CPU：18 - 23 | 5 |
| CPU：24 - 29 | 6 |
| CPU：30 - 35 | 7 |
| CPU：36 - 41 | 8 |
| CPU：42 - 47 | 9 |
| CPU：≥ 48 | 10 |

## ENI Limits

Based on CPU and memory configurations, the number of ENIs can be bound to a CVM differs from the number of private IPs can be bound to an ENI. The limits are shown in the following table:
> The number of IPs bound to a single ENI only represents the maximum number of IPs can be bound to an ENI. EIP quota is not based on this upper limit, but EIP [use limits](https://intl.cloud.tencent.com/document/product/213/5733).

| CVM Configuration               | Number of EIPs | Number of private IPs bound to a single ENI |
| ------------------- | :---- | :------ |
| CPU: 1 core   </br>Memory: 1GB    | 2     | 2       |
| CPU: 1 core  </br>Memory: > 1GB   | 2     | 6       |
| CPU: 2 cores            | 2     | 10      |
| CPU: 4 cores  </br>Memory: < 16GB | 4     | 10      |
| CPU: 4 cores   </br>Memory: > 16GB | 4     | 20      |
| CPU: 8 cores - 12 cores         | 6     | 20      |
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
	- If the fixed bandwidth you purchased is larger than 10 Mbps, public network inbound bandwidth distributed by Tencent Cloud will equal to the purchased bandwidth.
	- If the fixed bandwidth you purchased is less than 10 Mbps, Tencent Cloud will distribute 10 Mbps public network inbound bandwidth.

## Disk Limits

<table>
	<tr><th>Limit Type</th><th>Description</th></tr>
	<tr><td>Elastic cloud disk capability</td><td>Starting in May 2018, all data disks purchased with CVMs are elastic cloud disks, which support unmounting and remounting on CVMs. This feature is supported in all [availability zones](https://intl.cloud.tencent.com/document/product/213/35071). </td></tr>
	<tr><td>Cloud disk performance</td><td>I/O performance takes effect concurrently.<br/>For example, 1TB SSD has a maximum random IOPS of 26,000, meaning its IOPS for both read and write can reach this value. Due to performance limits, if the block size in this example is 4KB or 8KB, I/O can reach the maximum IOPS. If the block size is 16KB, I/O cannot reach the maximum IOPS (throughput has already reached the limit of 260MB/s).</td></tr>
	<tr><td>Number of elastic cloud disks can be mounted to a CVM</td><td>A maximum of 20.</td></tr>
	<tr><td>Number of snapshots in one region</td><td>64 + number of disks in the region * 64.</td></tr>
	<tr><td>Mounting cloud disks to CVM</td><td>The instance and cloud disks must be in the same availability zone.</td></tr>
	<tr><td>Snapshot rollback</td><td>Snapshot data can only be rolled back to the cloud disk where the snapshot was created.</td></tr>
	<tr><td>Type of cloud disks used to create snapshots</td><td>Only snapshots of data disks can be used to create new elastic cloud disks.</td></tr>
	<tr><td>Size of cloud disks used to create snapshots</td><td>The size of new cloud disks created from snapshots must be larger or equal to that of the source cloud disks.</td></tr>
	<tr><td>Repossessing cloud disks in arrears</td><td>For specific repossession mechanism, please see <a href="https://intl.cloud.tencent.com/document/product/362/31625">Arrears Reminder</a>.</td></tr>
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
<tr><th>Feature description</th><th>Limits</th></tr>
<tr><td>Number of security group</td><td>50 per region</td></tr>
<tr><td>Number of rules for a security group</td><td>100 (Inbound/Outbound)</td></tr>
<tr><td>Number of instances associated with a security group</td><td>100</td></tr>
<tr><td>Number of security groups associated with an instance</td><td>5</td></tr>
<tr><td>Number of rules that reference security group ID for each security group</td><td>10</td></tr>
</table>

## VPC Limits

| Resource | Limit | 
|---------|---------|
| Number of VPCs per region for each account | 5 | 
| Number of subnets per VPC | 10 |
| Number of basic network CVMs can be associated per VPC | 100 |
| Number of route tables per VPC | 10 |
| Number of routing tables associated with the subnet | 1 |
| Number of routing policies per route table | 100 |
| Number of default HAVIP per PVC | 10 |

