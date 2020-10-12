Before installing DTS-DBbridge, you need to set up the installation environment.

## Hardware Requirements
#### Basic configuration
- CPU: 8-core
- Memory: greater than 16 GB
- Disk capacity: greater than 500 GB

#### Recommended configuration
- CPU: 16-core
- Memory: greater than 32 GB
- Disk capacity: greater than 500 GB

## System Requirements
After the required hardware is ready, you need to install and configure the Linux operating system.

#### Supported system versions
CentOS/Red Hat versions 7.2 and later are supported. CentOS 7.2 is recommended.

#### Making sure the server time is correct
Check whether all servers have the same correct current time and time zone. If not, please reset them to their correct values.
```
date -R
```

## Obtaining an Installation Package
Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to obtain the latest installation package.

## Configuring a YUM Repository
Configure a YUM repository in the server where DTS-DBbridge is deployed. If you cannot access a YUM repository through the public network, you can configure a YUM repository locally or through the private network.
