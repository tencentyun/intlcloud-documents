Private network services are LAN services, where cloud services can access each other through internal linkages. Tencent Cloud services can access each other through [internet access](https://intl.cloud.tencent.com/document/product/213/5224) or the private network of Tencent Cloud. Tencent Cloud data centers are interconnected with underlying networks of megabytes/gigabytes. They enable communications via private networks with large bandwidth and low latency, which are free of charge if in the same region to help you build a network architecture flexibly.
## Private IP Address
### Overview
Private IPs are addresses that cannot be accessed through the Internet, based on which Tencent Cloud private networks are created. Each instance has a default network interface (i.e., eth0) for assigning private IPs. Private IPs can be automatically assigned by Tencent Cloud, or you can custom them (only under [VPC](https://intl.cloud.tencent.com/document/product/215/535)).
> If you change the private IP within the operating system, private network may be interrupted.
>

### Attributes
 - Private network is user-sensitive, and different users are isolated from each other. By default, cloud services of another user cannot be accessed via the private network.
 - Private network is region-sensitive, and different regions are isolated from each other. By default, cloud services under the same account in a different region cannot be accessed via the private network.

### Application Scenarios
Private IP can be used for the communication between CLBs and CVM instances, and between CVM instances and other Tencent Cloud services (such as TencentDB).

### Address Assignment
Each CVM instance will be assigned a default private IP address when started. The private IP varies by the [network environment](https://intl.cloud.tencent.com/document/product/213/5227):
 - Basic network: private IP address is automatically assigned by Tencent Cloud and cannot be changed.
 - VPC: Tencent Cloud VPC CIDR currently allows you to use one of the following IP ranges, and the maximum and minimum masks are /16 and /28:
  - **10.0**.0.0 - **10.255**.255.255
  - **172.16**.0.0 - **172.31**.255.255
  - **192.168**.0.0 - **192.168**.255.255

## Private Network DNS 
### DNS Server Address
Private network DNS service is used for domain name resolution. If DNS is configured incorrectly, domain name cannot be accessed.
Tencent Cloud provides reliable private network DNS servers in different regions. Specific configurations are shown below:
<table><tbody>
<tr><th>Network Environment</th><th>Region</th><th>Private Network DNS Server</th></tr>
<tr><td rowspan="14">Basic Network</td><td rowspan="4">Guangzhou</td><td>Guangzhou Zone 1: <br>10.112.65.31<br>10.112.65.32</td></tr>
<tr><td>Guangzhou Zone 2: <br>10.112.65.31<br>10.112.65.32</td></tr>
<tr><td>Guangzhou Zone 3: <br>10.59.218.193<br>10.59.218.194</td></tr>
<tr><td>Guangzhou Zone 4: <br>100.121.190.140<br>100.121.190.141</td></tr>
<tr><td>Shanghai</td><td>10.236.158.114<br>10.236.158.106</td></tr>
<tr><td>Beijing</td><td>10.53.216.182<br>10.53.216.198</td></tr>
<tr><td>North America</td><td>10.116.19.188<br>10.116.19.185</td></tr>
<tr><td>Hong Kong, China</td><td>10.243.28.52<br>10.164.55.3</td></tr>
<tr><td>Singpore</td><td>100.78.90.19<br>100.78.90.8</td></tr>
<tr><td>Guangzhou Open Zone</td><td>10.59.218.18<br>10.112.65.51</td></tr>
<tr><td>Chendu</td><td>100.88.222.14<br>100.88.222.16</td></tr>
<tr><td>Silicon Valley</td><td>100.102.22.21<br>100.102.22.30</td></tr>
<tr><td>Frankfurt</td><td>100.120.52.60<br>100.120.52.61</td></tr>
<tr><td>Seoul</td><td>10.165.180.53<br>10.165.180.62</td></tr>
<tr><td>VPC</td><td>All Regions</td><td>183.60.83.19<br>183.60.82.98</td></tr>
</tbody>
</table>

## Operation Guide
You can view or modify the private IP address of the instance. For detailed instructions, see:
- [Obtaining the Private IP Address of an Instance and Private Network DNS Settings](https://intl.cloud.tencent.com/document/product/213/17941)
- [Modifying Private IP Addresses](https://intl.cloud.tencent.com/document/product/213/16561)
