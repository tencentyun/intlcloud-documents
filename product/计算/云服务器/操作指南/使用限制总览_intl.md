## Account Limits for Purchasing CVM Instances

- You need to sign up for a Tencent Cloud account. For more information, please see [Sign up for Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) for registration instructions.
- You need to go through identity verification. For more information on how to verify your identity, please see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).
- When you create a postpaid CVM, the system will freeze the CVM fee for one hour. Make sure that the account has sufficient balance to pay for the order.

## Use Limits for CVM Instances

- Virtualized software cannot be installed or re-virtualized (such as installing VMware or Hyper-V).
- You cannot use sound card applications or external hardware devices (such as ISO files, USB disks, external disks and U-keys).
- The public gateway is available only in Linux systems.

## Purchase Limits for CVM Instances

- For each user in each availability zone, the **total quota** for postpaid CVM instances is 30.

- For more information, please see [Purchase Limits for CVM Instances](https://intl.cloud.tencent.com/document/product/213/2664).


## Image Limits

- Public image and service marketplace image: none.
- Custom image: Each region supports a maximum of 10 custom images.
- Shared image: Each custom image can be shared to a maximum of 50 Tencent Cloud users, and can only be shared to the accounts in the same region as the source account.
- For more information, please see [Image Type Limits](https://intl.cloud.tencent.com/document/product/213/4941).

## ENI Limits

- The number of ENIs bound to a CVM is quite different from that of private IPs bound to an ENI depending on the CPU and memory configurations. These allowed numbers are shown in the following table:

| CVM Configuration | Max. Number of ENIs | Max. Number of IPs Bound to Each ENI |
| ------------------- | :---- | :------ |
| CPU: 1-core   Memory: 1 GB    | 2     | 2       |
| CPU: 1-core   Memory: > 1 GB   | 2     | 6       |
| CPU: 2-core             |  2     | 10      |
| CPU: 4-core   Memory: < 16 GB | 4     | 10      |
| CPU: 4-core   Memory: > 16 GB | 4     | 20      |
| CPU: 8- to 12-core          | 6     | 20      |
| CPU: >12-core           |  8     | 30      |


## Bandwidth Limits

-  Upper Limit of the Outbound Bandwidth (Downstream Bandwidth):
<table border="3">
    <tr>
       <th rowspan="2"><b>Network Billing Method</b></th>
       <th colspan="2" ><b>CVM</b></th>
       <th rowspan="2"><b>Available range of the upper limit of bandwidth (Mbps)</b></th>
   </tr>
    <tr>
       <th><b>CVM Billing Method</b></th>
       <th><b>CVM Configuration</b></th>
    </tr>
	<tr>
	      <td rowspan="4">Bill-by-Traffic</td>
        <td >Postpaid CVM</td>
        <td >ALL</td>
				<td>0-100</td>    
   </tr>
	  <tr>
        <td rowspan="3">Prepaid CVM</td>
        <td>Cores ≤ 8</td>
				<td>0-200</td>        
   </tr>
	  <tr>
        <td>8 < Cores < 24</td>
        <td>0-400</td>
   </tr>
	 <tr>
        <td>Cores ≥ 24</td>
        <td>0-400 or no speed limit</td>
   </tr>
	 <tr>
		    <td rowspan="3">Bill-by-Bandwidth</td>
        <td >Postpaid CVM</td>
        <td >ALL</td>
				<td>0-100</td>      
   </tr>
	 <tr>
		    <td rowspan="2">Prepaid CVM</td>
        <td >Guangzhou Zone 1<br>Guangzhou Zone 2<br>Shanghai Zone 1<br>Hong Kong Zone 1<br>Toronto Zone 1</td>
				<td>0-200</td>      
   </tr>
	 <tr>
        <td>Other availability zones</td>
        <td>0-1,000</td>
   </tr>
    <tr>
		    <td>Shared bandwidth</td>
        <td colspan="2">ALL</td>
        <td>0-200 or no speed limit</td>    
    </tr>
</table>

-  Upper Limit of the Inbound Bandwidth (Upstream Bandwidth):

	- If the fixed bandwidth purchased by users is larger than 10 Mbps, Tencent Cloud assigns the public network inbound bandwidth that is equal to the purchased bandwidth.
	- If the fixed bandwidth purchased by users is less than 10 Mbps, Tencent Cloud assigns 10 Mbps public network inbound bandwidth.

## Disk Limits

| Limits on | Description |
| --- |  --- |
| Elastic cloud disk capability | Since May 2018, all the data disks bought with instances are all elastic cloud disks. You can unmount them from your CVM and get them remounted. This capability is available in all [Availability Zones](https://intl.cloud.tencent.com/doc/api/229/1286). |
| Cloud disk performance | The I/O performance described in the product documentation. For example, a 1 TB SSD cloud disk can deliver up to 24,000 random IOPS. This means the 24,000 IOPS is achievable for both read and write operations. The I/O performances of 4 KB/8 KB can both reach this number, while the IO of 16 KB cannot reach 24,000 IOPS because its throughput has already reached the limit of 260 MB/s. |
| Maximum number of cloud disks per instance | 20 at most |
| Number of snapshots in a single region | 64 + count of disks in the region * 64 |
| Mounting elastic cloud storage to CVM | The instance and the elastic cloud storage must be in the same availability zone. |
| Snapshot rollback | Snapshot data can only be rolled back to the cloud disk from which the snapshot was created. |
| Allowed disk type for creating elastic cloud disks using snapshots | You can only use data disk snapshots to create new elastic cloud disks. |
| Allowed disk size for creating elastic cloud disks using snapshots | The size of the created elastic cloud disk must be bigger or equal to the size of the cloud disk from which the snapshot was created. |

## Security Group Limits

- Security groups are region and project-specific. CVMs can only be associated with the security groups in the same region and project.
- Security groups apply to any CVM instances in network environment.
- Each user can set a maximum of 50 security groups for each project in each region.
- A maximum of 100 inbound/outbound access policies can be set for a security group.
- A CVM can be associated with multiple security groups, and a security group can be associated with multiple CVMs. No number limit is imposed.
- Security groups bound with CVMs in **basic network** **cannot filter** data packets sent from (or to) relational database (CDB) and cloud cache service (Redis and Memcached) of Tencent Cloud. If necessary, you can use iptables to filter traffic of such instances.
- The quota limits are as follows:

| Feature | Count |
|---------|---------|
| Security group | 50/Region |
| Access policy | 100 (Inbound/Outbound) |
| Number of instances associated with a security group | 100 |
| Number of security groups associated with an instance | 5 |
| Number of rules of a security group | 10 |

## VPC Limits

| Resource | Limit |
|---------|---------|
| Number of VPCs in a region |  5	 |
| Number of subnets per VPC |  10 |
| Number of basic network CVMs that can be associated with each VPC |  100 |
| Number of routing tables per VPC |  10	 |
| Number of routing policies per routing table |  100	 |
| Number of associated routing tables per subnet |  1 |
| Number of HAVIP per VPC | 10 |
