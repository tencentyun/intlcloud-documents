## Account Limits on CVM Instance Purchases

- You need a Tencent Cloud account. For more information about signing up for an account, refer to [Sign up for Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985).
- You need to verify your identity. For more information, refer to the [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).
- When you create a pay-as-you-go CVM instance, the system will put an hour’s worth of fees on hold to make sure your account has a sufficient balance to pay for the order.

## CVM Instances Use Limits

- Virtualization and hypervisor software (such as VMWare and Hyper-V) are not supported.
- Sound cards and directly attached external hardware devices (such as ISO files, USB disks, external disks, and U-keys) are not supported.
- Public network gateways only support Linux.

## CVM Instance Purchase Limits

- Each user can purchase up to **30** pay-as-you-go CVM instances in each availability zone.
- For more information, refer to [CVM Instance Purchase Limits](https://intl.cloud.tencent.com/document/product/213/2664).


## Image Limits

- Public Images: none.
- Custom images: each region supports a maximum of 10 custom images.
- Shared images: each custom image can be shared with a maximum of 50 Tencent Cloud users and only with accounts in the same region as the source account.
- For more information, refer to [Image Types Overview](https://intl.cloud.tencent.com/document/product/213/4941).

## Elastic IP (EIP) Limits

#### Quota Limits

| Resources | Limits |
|---------|:---------:|
| EIPs for each region of a Tencent Cloud account | 20 |
| Purchase applications for each region of a Tencent Cloud account per day | \* 2 |
| Free public IP reassignments when an EIP is disassociated per account per day | 10 |

#### CVM Public IP Assignment Limits

Starting from Sep. 18, 2019, the number of public IP addresses allowed for each CVM instance will vary according to the instance’s CPU configuration.
> CVM instances purchased prior to Sep. 18, 2019 will not be affected.
>
| Number of CPUs | Number of public IP addresses allowed (Public IPs and EIPs) |
|---------|---------|
| CPU: 1 - 5 | 2 |
| CPU: 6 - 11 | 3 |
| CPU: 8 - 12 | 4 |
| CPU: 18 - 23 | 5 |
| CPU: 24 - 29 | 6 |
| CPU: 30 - 35 | 7 |
| CPU: 36 - 41 | 8 |
| CPU: 42 - 47 | 9 |
| CPU: ≥ 48 | 10 |

## ENI Limits

The number of ENIs allowed for each CVM instance and the number of private IP addresses allowed for each ENI vary according to different CPU and memory configurations. The following table provides detailed:
> The number of IP addresses allowed for a single ENI does not mean your account has this EIP quota. For more information on how EIP quotas work, refer to [Elastic Public IP (EIP)](https://intl.cloud.tencent.com/document/product/213/5733).

| CVM instance configuration | ENIs | IPs per ENI |
| ------------------- | :---- | :------ |
| CPU: 1 core </br>Memory: 1 GB | 2 | 2 |
| CPU: 1 core </br>Memory: > 1 GB | 2 | 6 |
| CPU: 2 cores | 2 | 10 |
| CPU: 4 cores </br>Memory: < 16 GB | 4 | 10 |
| CPU: 4 cores </br>Memory: > 16 GB | 4 | 20 |
| CPU: 8 - 12 cores | 6 | 20 |
| CPU: > 12 cores | 8 | 30 |


## Bandwidth Limits

- Outbound Bandwidth (Downstream)
<table>
    <tr>
       <th rowspan="2"><b>Network billing method</b></th> 
       <th colspan="2" ><b>Instance</b></th>
       <th rowspan="2"><b>Bandwidth range (Mbps) </b></th>	
   </tr>
    <tr>
       <th><b>Instance billing method</b></th> 
       <th><b>Instance configuration</b></th> 
    </tr>
	<tr>
	      <td>Bill-by-traffic</td> 
        <td >Pay-as-you-go instance</td> 
        <td>ALL</td> 
				<td>0 - 100</td>    
   </tr>
	 <tr>
		    <td>Bill-by-bandwidth</td> 
        <td >Pay-as-you-go instance</td> 
        <td>ALL</td> 
				<td>0 - 100</td>      
   </tr>
    <tr>
		    <td>Shared bandwidth</td> 
        <td colspan="2">ALL</td> 
        <td>0 - 200 or unlimited</td>    
    </tr>
</table>

- Inbound Bandwidth (Upstream)
	- If you have purchased more than 10 Mbps of bandwidth, Tencent Cloud will match it when assigning your inbound bandwidth.
	- If you have purchased less than 10 Mbps of bandwidth, your inbound bandwidth is 10 Mbps.

## Disk Limits

<table>
	<tr><th>Type</th><th>Note</th></tr>
	<tr><td>Elastic Cloud Disks</td><td>Starting from May 2018, all data disks purchased with CVM instances are Elastic Cloud Disks, which can be mounted and unmounted from instances. This is available in all availability zones.</td></tr>
	<tr><td>Cloud disk performance limits | Read performance is the same as write performance <br/>For example, a 1 TB SSD with a maximum random IOPS of 26,000 means that its IOPS for both reads and writes can reach this value. Meanwhile, because of multiple performance limits, if the I/O block size is 4 KB/8 KB in this example, I/O can reach the maximum IOPS. If its block size is 16 KB, I/O cannot reach the maximum IOPS (throughput has already reached the limit of 260 MB/s). |
	<tr><td>Maximum Elastic Cloud Disk quota per instance</td><td>20</td></tr>
	<tr><td>Snapshot quota per region</td><td>64 + number of cloud disks in the region x 64</td></tr>
	<tr><td>Cloud disk mounting limit</td><td>The cloud disk and the CVM instance to which it is mounted must be in the same availability zone.</td></tr>
	<tr><td>Snapshot rollback limit</td><td>A snapshot can only be used to roll back the cloud disk from which it was generated.</td></tr>
	<tr><td>Cloud disk type limits for snapshots</td><td>Only data disk snapshots can be used to create new Elastic Cloud Disks.</td></tr>
	<tr><td>Cloud disk size limits for snapshots</td><td>Elastic Cloud Disks created from snapshots must be larger in size than the source cloud disk.</td></tr>
</table>


## Security Group Limits

- Security groups are located in regions. A CVM instance can be bound only to security groups in the same region.
- Security groups are applicable to CVM instances in any [network environment](https://intl.cloud.tencent.com/document/product/213/5227).
- Each user can set a maximum of 50 security groups for each project in each region.
A security group can contain a maximum of 100 inbound and 100 outbound access policies.
- A CVM instance can join multiple security groups, and one security group can be associated with multiple CVM instances.
- Security groups associated with CVM instances on the **basic network** **cannot filter** packets to or from Tencent Cloud relational databases and elastic caches (Redis and Memcached). If necessary, you can use iptables to filter these packets.
- The quota limits are as follows:
<table>
<tr><th>Item</th><th>Limit</th></tr>
<tr><td>Security group</td><td>50 per region</td></tr>
<tr><td>Access policy</td><td>Inbound: 100, outbound: 100</td></tr>
<tr><td>Number of CVM instances associated with a single security group</td><td>100</td></tr>
<tr><td>Number of security groups a CVM instance can be associated with</td><td>5</td></tr>
<tr><td>Number of security group IDs a security group can reference</td><td>10</td></tr>
</table>

## VPC Limits

| Resource | Limit |
|---------|---------|
| Number of VPCs per region for each account | 5 |
| Number of subnets per VPC | 10 |
| Number of basic network CVMs associated with a single VPC | 100 |
| Number of route tables per VPC | 10 |
| Number of routing tables a subnet can be associated with | 1 |
| Number of routing policies per route table | 100 |
| Default HAVIP quota per VPC | 10 |

