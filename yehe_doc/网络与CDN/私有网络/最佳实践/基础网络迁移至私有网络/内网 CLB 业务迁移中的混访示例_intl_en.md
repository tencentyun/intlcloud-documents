This document provides a sample configuration for the scenario that both the VPC and classic network are required during the business migration.


### Scenario
Resource configuration of the classic network-based business:
+ The CVM client accesses a private network CLB.
+ The private network CLB is bound with two CVMs (CVM 1 and CVM 2) as the real servers.
+ Applications deployed in CVM 1 and CVM 2 can access the backend TencentDB for MySQL services.

Requests:
+ Migrates resources from the classic network to a VPC
+ The VPC-based clients has a priority access to the private network CLB service in the classic network.
+ The classic network access remains available for one month after the migration.

### Migration process
<dx-steps>
- Create a VPC
- Migrate TencentDB services
- Configure a terminal connection
- Create a private network CLB and configure its backend service
- Configure a Classiclink
- Release the classic network resources
</dx-steps>


### Steps
1.  Create a VPC as instructed in [Creating VPCs](https://intl.cloud.tencent.com/document/product/215/31805).
2.  Migrate the TencentDB for MySQL services to the VPC as instructed in [Network Switch](https://intl.cloud.tencent.com/document/product/236/31915).
    >? During the migration, the TencentDB instance still connects. Both the original classic network IP and VPC IP addresses remain valid after the migration, thus maintaining your service availability.
    >
    ![]()
3.  Configure a terminal connection service to allow the CVM client in the VPC to access the public network CLB service in the classic network.
     ![]()
4.  Create a private network CLB instance and its real server in the VPC, and configure the related services.
   ![]()
5.  Configure a Classiclink to allow the classic network-based CVM to access the private network CLB instance in the VPC. Test whether the VPC provides services normally.
    ![]()
6.  After the VPC service is normal and VPC-based CVM starts accessing the private network CLB in the VPC, delete the terminal connection, maintain Classiclink, and release the resources in the classic network.
    ![]()

