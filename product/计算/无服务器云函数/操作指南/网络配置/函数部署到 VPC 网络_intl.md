If you want SCF to access private network resources such as CDB and CVM, you can change the network configuration when creating or editing a function to enable VPC access. Things to keep in mind:

* A function deployed in a VPC is isolated from the public network by default. If you want the function to have access to both private network and public network, you can add a NAT gateway to the VPC by following the steps in Granting a Function in VPC Access to Public Network.
* Currently, functions cannot be connected with resources on the basic network. If you need to access the basic network, you can contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1).

## Usage Scenario

* Access to private network services: This can be used to access products or services on the private network such as TencentDB for Redis and CKafka to ensure data and connection security.
* Access control: This can uniformly converge access requests from the public network to the same address and ensure the uniqueness of the egress address by means of the public network egress in the VPC.

## Editing Network Configuration

When creating or editing a function, you can find the VPC configuration on the function configuration page. Select the VPC to be accessed and the subnet you want to use.

By selecting `None` in the network option, you can switch the network environment of the function back to the current independent network environment.

## Viewing Network Configuration

After configuring the network of the function, you can view the specific configuration information in **Network** and **Subnet** in the function configuration.

## Using a VPC

After the configuration is completed and your VPC is started, the runtime network environment of the function will be switched from the current independent network environment to the VPC. When the function is started, it will use an IP address in a subnet of your VPC as the IP address of the function runtime environment.

> **Note** 
> Please make sure that there are enough free IP addresses available in the subnet. Otherwise, IP allocation will fail, causing the function startup to fail. You can increase the number of subnet IPs by changing the subnet mask length.



After the function is started, you can use code to access other products and services whose access entries are in the VPC through private IP addresses, such as [TencentDB for Redis](https://cloud.tencent.com/product/crs?idx=1), [TencentDB for CDB](https://cloud.tencent.com/product/cdb-overview), or CVM instances you configure in the VPC. The following is sample code to access [TencentDB for Redis](https://cloud.tencent.com/product/crs?idx=1), where the IP address of the Redis instance in the VPC is `10.0.0.86`.

```
# -*- coding: utf8 -*- 
import redis

def main_handler(event,context):
    r = redis.StrictRedis(host='10.0.0.86', port=6379, db=0,password="crs-i4kg86dg:abcd1234")
    print(r.set('foo', 'bar'))
    print(r.get('foo'))
    return r.get('foo')
```

After the function is switched to the VPC environment, it will lose its accessibility in the original independent network environment to the public network. If you need to continue to access the public network, you can [configure a public gateway](https://cloud.tencent.com/document/product/215/20078) or [a NAT gateway](https://cloud.tencent.com/document/product/552). For more information, see Granting a Function in VPC Access to Public Network.

### Name Server Configuration in a VPC

After configuring the VPC for the function, if you need to use domain names to access your self-built services in the VPC, you usually need to use a custom name server to implement domain name resolution.

In order to support the custom name server configuration in the SCF environment, you can implement the custom name server by configuring the `OS_NAMESERVER` environment variable.

| Environment variable name | Value setting rule | Purpose |
| --- | --- | --- |
| OS_NAMESERVER | It can be one or more IP addresses or domain names, separated by ";". A maximum of 5 custom name servers can be configured. | Configure a custom name server |

The configuration can be checked for effect by printing out the /etc/resolv.conf file.

```
with open("/etc/resolv.conf") as f:
    print(f.readlines())
```



