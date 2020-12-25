Instance metadata refers to data relevant to an instance. It can be used for configuring or managing a running instance.
>? Although instance metadata can only be accessed after login, the data has not been encrypted. Anyone who accesses the instance can view its metadata. Therefore, you should take proper actions to protect sensitive data (for example, using a permanent encryption key).
>


## Overview
Tencent Cloud provides the following metadata:

| Name | Description | version |
|---------|---------|---------|
| instance-id | Instance ID | 1.0 |
| instance-name | Instance name | 1.0 |
| uuid | Unique instance ID | 1.0 |
| local-ipv4 | Instance private IP address | 1.0 |
| public-ipv4 | Instance public IP address | 1.0 |
| mac | MAC address of the instance's eth0 device | 1.0 |
| placement/region | Instance region | Updated on September 19, 2017 |
| placement/zone | Instance availability zone | Updated on September 19, 2017 |
| network/interfaces/macs/**${mac}**/mac | Instance network interface MAC address | 1.0 |
| network/interfaces/macs/**${mac}**/primary-local-ipv4 | Instance network interface primary private IP | 1.0 |
| network/interfaces/macs/**${mac}**/public-ipv4s | Instance network interface public IP address | 1.0 |
| network/interfaces/macs/**${mac}**/vpc-id | Instance network interface VPC ID | Updated on September 19, 2017 |
| network/interfaces/macs/**${mac}**/subnet-id | TInstance network interface subnet ID | Updated on September 19, 2017 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/gateway | Instance network interface gateway address | 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/local-ipv4 | Instance network interface private IP address | 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/public-ipv4 | Instance network interface public IP address | 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/public-ipv4-mode | Instance network interface public network mode | 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/subnet-mask | Instance network interface subnet mask | 1.0 |
| payment/charge-type | Instance billing plan | Updated on September 19, 2017 |
| payment/create-time | Instance creation time | Updated on September 19, 2017 |
| payment/termination-time | Instance termination time | Updated on September 19, 2017 |
| app-id | AppID of the user to which the instance belong | Updated on September 19, 2017|
| as-group-id | Auto scaling group ID of the instance | Updated on September 19, 2017 |
| spot/termination-time | Spot instance termination time | Updated on September 19, 2017 |
| /meta-data/instance/instance-type | Instance type | Updated on September 19, 2017|
| /instance/image-id | Instance image ID | Updated on September 19, 2017 |
| /instance/security-group | Information of the security group bound to the instance | Updated on September 19, 2017 |


>? Fields `${mac}` and `${local-ipv4}` in the above table indicate the mac address and private IP address of the specified network interface, respectively.
> 
> The destination URL address of the request is case-sensitive. You must construct the destination URL address of a new request according to the returned result of the request.
>
> The returned data of placement is changed in the new version. To use the data in the previous version, specify the previous version path or leave the version path empty to access the data of version 1.0. For more information on the returned data of placement, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091).

## Querying Instance Metadata
After logging in to an instance, you can access the metadata such as its local IP address and public IP address to manage connections with external applications.
To view all the instance metadata within a running instance, use the following URI:

```
http://metadata.tencentyun.com/latest/meta-data/
```
You can access the metadata by using cURL or an HTTP GET request, for example:

```
curl http://metadata.tencentyun.com/latest/meta-data/
```
* For resources that do not exist, the HTTP error code "404 - Not Found" will be returned.
* To operate on the instance metadata, please first log in to the instance. For more information, see [Logging in to a Windows Instance Using the RDP File (Recommended)](https://intl.cloud.tencent.com/document/product/213/5435) and [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).

### Sample metadata query

The following shows how to obtain the metadata version.
>! When Tencent Cloud modifies the metadata access path or returned data, a new metadata version is released. If your application or script relies on the structure or returned data of a previous version, you can specify that version. If no version is specified, version 1.0 is used by default.
>

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/
1.0
2017-09-19
latest
meta-data
```

The following shows how to view the metadata root directory. The lines ending with / represent directories and the ones that do not represent the accessed data. For the description of accessed data, refer to the aforementioned **Overview**.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/
instance-id
instance-name
local-ipv4
mac
network/
placement/
public-ipv4
uuid
```

The following shows how to obtain the physical location information of an instance. For the relationship between the returned data and the physical location, refer to [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091).

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/region
ap-guangzhou

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/zone
ap-guangzhou-3
```

The following shows how to obtain the private IP address of an instance. If an instance has multiple ENIs, the network address of eth0 is returned.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/local-ipv4
10.104.13.59
```

The following shows how to obtain the public IP address of an instance.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/public-ipv4
139.199.11.29
```

The following shows how to obtain an instance ID. The instance ID is used to uniquely identify an instance.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/instance-id
ins-3g445roi
```

The following shows how to query the instance UUID. The instance UUID can also be used as the unique identifier of an instance, but we recommend that you use instance ID to identify instances.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/uuid
cfac763a-7094-446b-a8a9-b995e638471a
```

The following shows how to obtain the MAC address of an instance's eth0 device.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/mac
52:54:00:BF:B3:51
```

The following shows how to obtain the ENI information of an instance. In case of multiple ENIs, multiple lines of data are returned, with each line indicating the data directory of an ENI.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/
52:54:00:BF:B3:51/
```

The following shows how to obtain the information of a specified ENI.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/
local-ipv4s/
mac
vpc-id
subnet-id
owner-id
primary-local-ipv4
public-ipv4s
local-ipv4s/
```

The following shows how to obtain the VPC information of a specified ENI.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/vpc-id
vpc-ja82n9op

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/subnet-id
subnet-ja82n9op
```

The following shows how to obtain a list of private IP addresses bound to the specified ENI. If the ENI is bound with multiple private IP addresses, multiple lines of data are returned.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/
10.104.13.59/
```

The following shows how to obtain the information of a private IP address.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59
gateway
local-ipv4
public-ipv4
public-ipv4-mode
subnet-mask
```

The following shows how to obtain the gateway of a private IP address. This data is only available for VPC models. For more information, see [Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215).

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/gateway
10.15.1.1
```

The following shows how to obtain the public network access mode of a private IP address. This data is only available for VPC models. A classic network CVM accesses the public network through the public gateway.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4-mode
NAT
```

The following shows how to obtain the public IP address bound to a private IP address.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4
139.199.11.29
```

The following shows how to obtain the subnet mask of a private IP address.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/subnet-mask
255.255.192.0
```

The following shows how to obtain the billing plan of an instance.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/charge-type
POSTPAID_BY_HOUR
```

The following shows how to obtain the creation time of an instance.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/create-time
2018-09-18 11:27:33
```

The following shows how to obtain the instance termination time (only available to monthly-subscribed instances）

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/termination-time
2018-10-18 11:27:33
```

The following shows how to obtain the spot instance termination time.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/spot/termination-time
2018-08-18 12:05:33
```

The following shows how to obtain the account AppID of the CVM.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/app-id
123456789
```

## Querying Instance User Data
You can specify instance user data when creating an instance. CVM instances with cloud-init configured can access the data.

### Searching user data
After login, you can access user data by using the following method.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/user-data
179, client, shanghai
```
