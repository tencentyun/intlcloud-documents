# Using TCCLI

## Operation Scenarios

TCCLI integrates all the products on Tencent Cloud international website that support TencentCloud API and allows for configuration and management of such products. For example, you can use TCCLI to create and manage a CVM instance, create a CBS disk and view its usage, and create a VPC and add resources to it. All operations that can be done on console pages can be performed by running commands in TCCLI.

- Run the `tccli cvm DescribeInstances` command to see what CVM instances are under the current account.
- Run the `tccli cbs DescribeDisks` command to view the list of CBS disks.

## Operation Examples

> Note:
>
> Please note that the non-simple parameters in the demo must be in standard json format.

Take creating a CVM instance as an example:
Mac and Linux:

```bash
tccli cvm RunInstances --InstanceChargeType POSTPAID_BY_HOUR --Placement '{"Zone":"ap-guangzhou-2"}' --InstanceType S1.SMALL1 --ImageId img-8toqc6s3 --SystemDisk '{"DiskType":"CLOUD_BASIC", "DiskSize":50}' --InternetAccessible '{"InternetChargeType":"TRAFFIC_POSTPAID_BY_HOUR","InternetMaxBandwidthOut":10,"PublicIpAssigned":true}' --InstanceCount 1 --InstanceName TCCLI-TEST --LoginSettings '{"Password":"P1easeChange1t@"}' --HostName TCCLI-HOST-NAME1
```
Windows：

```bash
tccli cvm RunInstances --InstanceChargeType POSTPAID_BY_HOUR --Placement {\"Zone\":\"ap-guangzhou-2\"} --InstanceType S1.SMALL1 --ImageId img-8toqc6s3 --SystemDisk {\"DiskType\":\"CLOUD_BASIC\", \"DiskSize\":50} --InternetAccessible {\"InternetChargeType\":\"TRAFFIC_POSTPAID_BY_HOUR\",\"InternetMaxBandwidthOut\":10,\"PublicIpAssigned\":true} --InstanceCount 1 --InstanceName TCCLI-TEST --LoginSettings {\"Password\":\"P1easeChange1t@\"} --HostName TCCLI-HOST-NAME1
```
> Note:
>
> For details of more functions, you can view the supported products by running the `tccli help` command, view the supported APIs by running the `tccli cvm help` command (with CVM as an example), and view the parameters supported by APIs by running the `tccli cbs DescribeDisks help` command (with the DescribeDisks API of CBS as an example).
