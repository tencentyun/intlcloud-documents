
Tencent Cloud VPC can be integrated with many other Tencent Cloud Services. The relationships between them are shown in the following table:

## 1. Compute and Network Services

| Product | Relationship with VPC |
|---------|---------|
| [Cloud Virtual Machine (CVM)](https://intl.cloud.tencent.com/product/cvm.html) | You can deploy the CVM in the VPC |
| [Cloud Load Balance (CLB)](https://intl.cloud.tencent.com/product/clb.html?idx=2) | You can deploy private network LB or public network LB in a private network |
|  NAT Gateway | It can be used to access the Internet with traffic in the VPC|
| [VPN Connections](https://intl.cloud.tencent.com/product/vpn.html) | Connect VPC and user's IDC via IPsec VPN |
| [Direct Connect (DC)](https://intl.cloud.tencent.com/product/dc.html) | Connect VPC and user's IDC via Direct Connect |
| Basic Cloud Monitor (BCM) | Provide custom alarms for the key metrics of certain services in the VPC |

## 2. Database Services
| Product | Relationship with VPC |
|---------|---------|
| [CDB for MySQL](https://intl.cloud.tencent.com/product/cdb.html) | You can deploy the database service in the VPC. This service will consume the IP resources of VPC |
| [CDB for SQL Server](https://intl.cloud.tencent.com/product/sqlserver.html) | Same as above |
| [CDB for TDSQL](https://intl.cloud.tencent.com/product/cdb.html) | Same as above |
| [CDB for PostgreSQL](https://intl.cloud.tencent.com/product/postgresql.html) | Same as above |
| Cloud Cache Service Memcached | Same as above |
| [Cloud MongoDB Service](https://intl.cloud.tencent.com/product/mongodb.html) | Same as above |
