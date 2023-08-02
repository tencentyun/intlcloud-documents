This document describes the momentary disconnection prevention feature of the TencentDB for MySQL database proxy.

## Background
During the instance Ops, you may need to make some adjustments, such as configuration modification, planned HA switch, and planned restart. Theses Ops may cause the problems, such as session interruption, momentary disconnection and failed new connections. The TencentDB for MySQL database proxy provides the momentary disconnection prevention feature that enables lossless application continuity to prevent disconnection and transaction interruption.

## How It Works
The momentary disconnection prevention feature implements MySQL’s session track mechanism. When the lossy behavior is perceived, the database proxy will disconnect the client from the source node before the switch, and connect to the source node after the switch. Then the session-related system variables, user variables, and character set encoding information will be transferred to the new backend connection through the session track mechanism, so as to realize the lossless switching on the application side.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/cJuQ313_%E4%BA%91%E6%95%B0%E6%8D%AE%E5%BA%93%20MySQL_%E6%B5%81%E7%A8%8B%E5%9B%BE_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US.png)

## Notes
- If the statement uses the temp tables associated with each session, the connection cannot be recovered, and an error will be reported.
- To use the momentary disconnection prevention feature, you need to upgrade the database proxy kernel version to v1.3.1 or later.
- The disconnection prevention feature will stop the transactions over 3 seconds.
- When the connection is switched, if the database proxy is receiving the result message from the database, only part of the data will be transferred due to the source/replica switch, and the momentary disconnection prevention feature will be disabled.

## Performance Testing
The performance test of the momentary disconnection prevention feature for Tencent DB for MySQL database proxy is described in the following.

### Test environment
- Region/AZ: Beijing - Beijing Zone 7
- Client: S5.8XLARGE64 (32-core 64 GB Standard S5)
- Client operating system: CentOS 8.2 64-bit
- Network: Both the CVM and TencentDB for MySQL instances are in the same VPC subnet.

The information of the tested TencentDB for MySQL instance is as follows:
- Storage type: Local SSD disk
- Instance type: General
- Parameter template: High-performance template

### Test tool
SysBench, as the tool for the performance test, is a modular, cross-platform, and multi-threaded benchmark tool for evaluating OS parameters that are important for a system running a database under intensive load. The idea of this benchmark suite is to quickly get an impression about system performance without setting up complex database benchmarks or even without installing a database at all.

### Test method
In different Ops scenarios, you can analyze the ratio of momentary disconnections before and after the operation to test whether a database proxy provides momentary disconnection prevention for the high-availability MySQL instance.

## Test Results
In the following Ops scenarios, the high-availability MySQL instance maintains a 100% connection keep-alive rate by the momentary disconnection prevention capability of the database proxy.

| Ops scenario | Keep-alive rate |
|---------|---------|
| Performing source-replica switch | 100% |
| Upgrading kernel minor version | 100% |
| Adjusting the instance specifications | 100% |

