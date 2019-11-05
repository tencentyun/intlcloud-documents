This document describes the rule limits for security groups.
- Security groups are divided by region. A Cloud Virtual Machine (CVM) can be bound only to the security groups in the same region.
- Security groups are applicable to CVM instances in any [network environment](https://intl.cloud.tencent.com/document/product/213/5227).
- Each user can set a maximum of 50 security groups for each project in a region.
- A maximum of 100 inbound or outbound access rules can be set for each security group.
- One CVM can join multiple security groups, and one security group can be associated with multiple CVMs.
- Security groups associated with CVMs on a **basic network** are **not able to filter** packets from or towards Tencent Cloud relational databases and elastic cache (Redis and Memcached). If necessary, you can use iptables to filter traffic for such instances.
- The quota limits are as follows:
<table>
<tr><th>Item</th><th>Quota</th></tr>
<tr><td>Security group</td><td>50 per region</td></tr>
<tr><td>Access policy</td><td>Inbound: 100, outbound: 100</td></tr>
</table>

