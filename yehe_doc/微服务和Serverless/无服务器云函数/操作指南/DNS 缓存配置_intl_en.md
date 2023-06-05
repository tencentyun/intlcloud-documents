

## Overview

When the client initiates an access request to an address, it will query whether the local DNS cache has relevant records, and if so, it will directly access the corresponding IP; otherwise, it will delegate global query to the recursive server.

As DNS resolution uses the UDP protocol for communication, it is greatly affected by the network environment and may have a delay of several seconds in extreme conditions. In SCF use cases, the domain resolution delay may cause function execution failures due to timeout and affect the normal business logic. When a function is invoked frequently, the DNS server's resolution frequency may exceed the limit, which also will cause function execution failures.

SCF offers DNS caching configuration to solve the above problems. DNS caching can improve the domain resolution efficiency and increase the domain resolution success rate by mitigating network jitters.

## Use Cases
 This feature is applicable to scenarios where an address is requested in the function code and the function is invoked frequently.

## Directions

As code deployment-based event-triggered functions, HTTP-triggered functions, and image deployment-based functions have different implementation mechanisms, you should enable DNS caching in the corresponding steps:

### Code deployment-based event-triggered function

1. Log in to the [Serverless console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) and select the target function to enter the function details page.
2. On the function configuration page, click **Edit** in the top-right corner and select **Enable DNS Caching**.
3. Click **Save**.

   

### HTTP-triggered function

1. Add the following command to the HTTP-triggered function's bootstrap file [scf_bootstrap](https://intl.cloud.tencent.com/document/product/583/40690) to start the nscd process and enable DNS caching:
``` shell
/var/lang/bin/nscd -f /var/lang/conf/nscd.conf
```
2. Deploy the updated `scf_bootstrap` and the function code together in the cloud. Then, DNS caching will be enabled for new invocations.

### Image deployment-based function

1. Install nscd during image creation. Taking CentOS as an example, you can run the following command to install nscd:
```
yum install nscd -y
```
2. Update the default `/etc/nscd.conf` file with the following content:
``` 
#
# /etc/nscd.conf
#
# An example Name Service Cache config file. This file is needed by nscd.
#
# WARNING: Running nscd with a secondary caching service like sssd may lead to
# unexpected behaviour, especially with how long entries are cached.
#
# Legal entries are:
#
# logfile <file>
# debug-level <level>
# threads <initial #threads to use>
# max-threads <maximum #threads to use>
# server-user <user to run server as instead of root>
# server-user is ignored if nscd is started with -S parameters
# stat-user <user who is allowed to request statistics>
# reload-count unlimited|<number>
# paranoia <yes|no>
# restart-interval <time in seconds>
#
# enable-cache <service> <yes|no>
# positive-time-to-live <service> <time in seconds>
# negative-time-to-live <service> <time in seconds>
# suggested-size <service> <prime number>
# check-files <service> <yes|no>
# persistent <service> <yes|no>
# shared <service> <yes|no>
# NOTE: Setting 'shared' to a value of 'yes' will accelerate the lookup,
# but those lookups will not be counted as cache hits
# i.e. 'nscd -g' may show '0%'.
# max-db-size <service> <number bytes>
# auto-propagate <service> <yes|no>
#
# Currently supported cache names (services): passwd, group, hosts, services
#
# logfile /var/log/nscd.log
# threads 4
# max-threads 32
server-user root
# stat-user somebody
debug-level 0
reload-count 2
paranoia no
# restart-interval 3600
enable-cache passwd no
positive-time-to-live passwd 600
negative-time-to-live passwd 20
suggested-size passwd 211
check-files passwd yes
persistent passwd yes
shared passwd yes
max-db-size passwd 33554432
auto-propagate passwd yes
enable-cache group no
positive-time-to-live group 3600
negative-time-to-live group 60
suggested-size group 211
check-files group yes
persistent group yes
shared group yes
max-db-size group 33554432
auto-propagate group yes
enable-cache hosts yes
positive-time-to-live hosts 300
negative-time-to-live hosts 0
suggested-size hosts 211
check-files hosts no
persistent hosts no
shared hosts yes
max-db-size hosts 8388608
enable-cache services no
positive-time-to-live services 600
negative-time-to-live services 3
suggested-size services 211
check-files services yes
persistent services yes
shared services yes
max-db-size services 33554432
enable-cache netgroup no
positive-time-to-live n etgroup 28800
negative-time-to-live netgroup 20
suggested-size netgroup 211
check-files netgroup yes
persistent netgroup yes
shared netgroup yes
max-db-size netgroup 33554432
```
3. Add the following command to the bootstrap file `scf_bootstrap` to start nscd process and enable DNS caching.
 Taking CentOS as an example, add the following command to the bootstrap file:
```shell
${PATH}/nscd -f /etc/nscd.conf 
```
>! `${PATH}` is the absolute path where nscd is installed.
