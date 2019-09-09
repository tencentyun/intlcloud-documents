
After an instance is initialized, you need to enter the set password when connecting to Redis.

## Standard Edition Connection
The Standard Edition supports 2 connection formats:
Format 1: "Instance ID:password". For example, if your instance ID is crs-bkuza6i3 and password is abcd1234, then the connection command is as follows:
`redis-cli -h IP address -p port -a crs-bkuza6i3:abcd1234`

Format 2: Open-source format. For example, if the password you set is abcd1234, then the connection command is as follows:
`redis-cli -h IP address -p port -a abcd1234`

>- **Standard Edition (community)**:
 It supports access format 1.
 Only instances of the Standard Edition (Community) purchased after June 28, 2017 support access format 2.
>- **Standard Edition (CKV)**:
It only supports access format 1.


## Cluster Edition Connection
> Instances of the legacy Cluster Edition (purchased before January 1, 2018) and the Cluster Edition (CKV) support the following password format:
>"Instance ID:password". For example, if your instance ID is crs-bkuza6i3 and password is abcd1234, then the connection command is as follows:
`redis-cli -h IP address -p port -a crs-bkuza6i3:abcd1234`

The Cluster Edition (Community) supports the following password format:
Open-source format. For example, if the password you set is abcd1234, then the connection command is as follows:
`redis-cli -h IP address -p port -a abcd1234`

## Connection Example
For examples of each connection format, see [Connecting to an instance](https://intl.cloud.tencent.com/document/product/239/7042).

