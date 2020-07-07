## Operation Scenarios
Tencent Cloud SCF id deployed in the public network by default. This document describes how to enable SCF to access resources in the private network through VPC configuration, such as TencentDB, CVM, TencentDB for Redis, and CKafka, which helps ensure data and connection security.


## Notes
When configuring a VPC, pay attention to the following points:
- A function deployed in a VPC is isolated from the public network by default. If you want the function to have access to both private network and public network, you can do so in the following two ways:
 - Configure the public network access of SCF and make sure that the egress address for public network access is unique.
 - Add an NAT gateway through VPC. For more information, please see [Configuring NAT in VPC](https://intl.cloud.tencent.com/document/product/583/19704).
- Currently, functions cannot be connected with resources on the basic network.


## Prerequisites
You have [created a function](https://intl.cloud.tencent.com/document/product/583/32742).


## Directions
### Modifying network configuration
1. Log in to the Serverless Cloud Function Console and click **Function Service**(https://console.cloud.tencent.com/scf/list) in the left sidebar.
2. Select the region at the top of the page and click the name of the function to be configured.
3. On the "Function Configuration" page, click **Edit** in the top-right corner.
4. Set **VPC** to "Enable", and select the VPC and subnet you want to use.


### Using VPC
After you configure the private network access for a function and start to use the VPC, the function will switch from the current independent network environment to the configured VPC. When the function starts, an IP address in your VPC subnet will be used as the IP address of the function runtime environment. In order to reduce the functions' usage of subnet IP addresses, running function instances will share a proxy pair and scale the proxy pair based on the network bandwidth utilization.

After the function is started, you can use code and private IP address to access resources whose access entries are in the VPC, such as [TencentDB for Redis](https://intl.cloud.tencent.com/product/crs?idx=1), TDSQL, and CVM.
The following is sample code to access [TencentDB for Redis](https://intl.cloud.tencent.com/product/crs?idx=1), where the IP address of the Redis instance in the VPC is `10.0.0.86`.
```python
# -*- coding: utf8 -*-
import redis
def main_handler(event,context):
    r = redis.StrictRedis(host='10.0.0.86', port=6379, db=0,password="crs-i4kg86dg:abcd1234")
    print(r.set('foo', 'bar'))
    print(r.get('foo'))
    return r.get('foo')
```

#### Name server configuration in VPC
After configuring private network access for a function, if you want to use domain names to access your self-built services in the VPC, you usually need to use a custom `name server` to implement domain name resolution.
In order to support the custom `name server` configuration in the SCF environment, you can implement the custom `name server` by configuring the `OS_NAMESERVER` environment variable as shown below:

<table>
	<tr>
	<th>Environment Variable Name</th>
  <th>Value Rule</th>
	<th>Feature</th>
	</tr>
	<tr>
	<td>OS_NAMESERVER</td>
	<td>
		<ul style="margin-bottom:0px;"> 
		<li>It can be one or more IP addresses or domain names separated by <code>;</code>.</li>
			<li>A maximum of 5 custom <code>name servers</code> can be configured.</li>
		<ul>
	</td>
	<td>Configures custom <code>name server</code>.</td>
	</tr>
</table>


#### Verifying configuration
As shown in the following code, the configuration can be checked for effect by printing out the `/etc/resolv.conf` file.
```python
with open("/etc/resolv.conf") as f:
    print(f.readlines())
```

## Relevant Operations
### Viewing network configuration
1. Log in to the Serverless Cloud Function Console and click **Function Service**(https://console.cloud.tencent.com/scf/list) in the left sidebar.
2. Select a region at the top of the page and click the name of a function for which private network access has been configured to view the specific configuration through the corresponding **network** and **subnet**.
