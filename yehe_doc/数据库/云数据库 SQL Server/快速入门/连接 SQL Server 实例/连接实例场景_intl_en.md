This document describes some scenarios and methods of connecting to a TencentDB for SQL Server instance from a Windows CVM instance or local Windows system through SQL Server Management Studio (SSMS). For detailed directions, see [Connecting to TencentDB for SQL Server Instance from Windows CVM Instance](https://intl.cloud.tencent.com/document/product/238/11626) and [Connecting to TencentDB for SQL Server Instance from Local System](https://intl.cloud.tencent.com/document/product/238/11627).

## Connecting to a TencentDB for SQL Server Instance from a Windows CVM Instance
### Scenario 1
The CVM and TencentDB for SQL Server instances are in the same VPC or classic network in the same region under the same Tencent Cloud root account.
**Example**: Under account 1, the CVM instance is in subnet A in VPC 1 in Guangzhou region, and the TencentDB for SQL Server instance is in subnet B in VPC 1 in Guangzhou region.
**Connection method**: Connect them over the private network.

### Scenario 2
The CVM and TencentDB for SQL Server instances are in different VPCs in the same region under the same Tencent Cloud root account.
**Example**: Under account 1, the CVM instance is in subnet A in VPC 1 in Guangzhou region, and the TencentDB for SQL Server instance is in subnet B in VPC 2 in Guangzhou region.
**Connection method**: We recommend that you connect them through [CCN](https://intl.cloud.tencent.com/document/product/1003/31985).

### Scenario 3
The CVM and TencentDB for SQL Server instances are in different regions under the same Tencent Cloud root account.
**Example**: Under account 1, the CVM instance is in subnet A in VPC 1 in Guangzhou region, and the TencentDB for SQL Server instance is in subnet B in VPC 2 in Beijing region.
**Connection method**: We recommend that you connect them through [CCN](https://intl.cloud.tencent.com/document/product/1003/31985).

### Scenario 4
The CVM and TencentDB for SQL Server instances are under different Tencent Cloud root accounts.
**Example**: The CVM instance is in subnet A in VPC 1 in Guangzhou region under account 1, and the TencentDB for SQL Server instance is in subnet B in VPC 2 in Beijing region under account 2.
**Connection method**: We recommend that you connect them through [CCN](https://intl.cloud.tencent.com/document/product/1003/31985).

## Connecting to a TencentDB for SQL Server Instance from a Local Windows System
### Two-node (formerly High Availability/Cluster Edition) instance
- Option 1: Use [VPN](https://intl.cloud.tencent.com/document/product/1037/32679), or [Direct Connect](https://intl.cloud.tencent.com/document/product/216/7557), or [CCN](https://intl.cloud.tencent.com/document/product/1003/31985) for interconnection, which are more secure and stable.
- Option 2: Connect to the instance over the public network by enabling the public network address or binding the instance to CLB to enable public network access in the console as instructed in [Connecting to TencentDB for SQL Server Instance from Local System](https://intl.cloud.tencent.com/document/product/238/11627).
- Option 3: Use a Linux CVM instance with a public IP to map the ports as instructed in [Connecting to TencentDB for SQL Server Instance from Local System](https://intl.cloud.tencent.com/document/product/238/11627#WWIPLJSL).

### Single-node (formerly Basic Edition) instance
- Option 1: Use [VPN](https://intl.cloud.tencent.com/document/product/1037/32679), or [Direct Connect](https://intl.cloud.tencent.com/document/product/216/7557), or [CCN](https://intl.cloud.tencent.com/document/product/1003/31985) for interconnection, which are more secure and stable.
- Option 2: Connect to the instance over the public network by enabling the public network address in the console as instructed in [Connecting to TencentDB for SQL Server Instance from Local System](https://intl.cloud.tencent.com/document/product/238/11627#kqwwdz).
- Option 3: Use a Linux CVM instance with a public IP to map the ports as instructed in [Connecting to TencentDB for SQL Server Instance from Local System](https://intl.cloud.tencent.com/document/product/238/11627#WWIPLJSL).
