
## Scenario

Online migration is a service migration method that supports migrating physical machines, virtual machines, and third-party cloud servers to Tencent Cloud CVM, making it easy for you to deploy a unified platform for computing resources or build a hybrid cloud across different platforms.
This document guides you through how to use online migration.
>The source server mentioned in this page can be a physical server, virtual machine, or cloud server on another cloud platform such as AWS, Microsoft Azure, Google Cloud Platform, Alibaba Cloud, and Huawei Cloud.

## Application Scenarios

Online migration is suitable for the following scenarios:
- Migrate physical servers, virtual machines, and third-party cloud servers to CVM.
- Complete service migration without interrupting your business.

### Differences from Offline Migration

Data of the current running environment on the source server can be migrated to the destination server without service interruption. Throughout the entire process, you can completely store the running state of the source server and restore it to the original or even another hardware platform. After restoration, the virtual machine can still run smoothly with no perceptible differences in the usage of the service.

## Supported OS

Operating systems supported for online migration include without limitation the following (32-bit or 64-bit):

| Linux     |    Windows |  
| -------- | --------|
| <ul><li>CentOS 5/6/7</li><li>Ubuntu 10/12/14/16/17</li><li>Debian 7/8/9</li><li>SUSE 11.4/12.1/12.2</li><li>openSUSE 13.1</li></ul>   |   <ul><li>Windows Server 2016</li><li>Windows Server 2012</li><li>Windows Server 2008</li><li>Windows Server 2003</li></ul> |


## Prerequisites

- Register a Tencent Cloud account and prepare the destination CVM instance.
- Contact your Tencent Cloud sales rep or submit a ticket to request the permission and migration tool installation package and install it on the source server (i.e., the server to be migrated).

## Directions

1. Use the migration tool to check the information such as configuration and network connection of the source server and the destination server to determine whether migration is possible.
2. Send the request through an API, and the console puts the destination server (i.e., CVM instance) in "waiting for migration" status.
3. Perform an incremental system disk migration until the tool determines that the migration is completed.

For more information, see the Online Service Migration Guide in the migration toolkit.


