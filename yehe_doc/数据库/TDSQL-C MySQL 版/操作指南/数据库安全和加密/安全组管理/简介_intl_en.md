This document describes the concepts and descriptions of security groups.

## What is a security group?
A [security group] (https://intl.cloud.tencent.com/document/product/213/12452) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for instances of CVM, CLB and TencentDB. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list.

## Security Group Rules and Limits
- For more information on security group rule, see [Security Group](https://intl.cloud.tencent.com/document/product/213/12452).
- For use limits and quotas of security groups, see [Use Limits > Security Group Limits](https://intl.cloud.tencent.com/document/product/213/15379).

## Security Group Description
- TencentDB-C for MySQL security groups currently only support network access control for VPCs and public networks but not the classic network.
- Security groups associated with TencentDB instances in the Frankfurt, Silicon Valley, and Singapore regions currently do not support public network access control.
- As TencentDB doesn’t have any active outbound traffic, outbound rules don’t apply to it.
- TDSQL-C for MySQL security groups support read-write and read-only instances.

## TDSQL-C for MySQL Security Group Operations
- [Creating and Managing TencentDB Security Groups](https://www.tencentcloud.com/document/product/1098/52007)
- [Modifying/Adding Security Group Rules](https://www.tencentcloud.com/document/product/1098/52744)
- [Configuring Security Groups for TencentDB](https://www.tencentcloud.com/document/product/1098/44594)。
