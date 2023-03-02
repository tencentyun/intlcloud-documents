## Overview

Kerberos is a unified authentication service widely used in the big data ecosystem. GooseFS, as the storage acceleration service for big data and data lake scenarios, allows you to connect cluster nodes and user access requests to Kerberos. This document describes how to configure GooseFS connection to Kerberos and how to use a Hadoop Delegation Token for authentication.

## Connecting GooseFS to the Kerberos Authentication Architecture

![](https://qcloudimg.tencent-cloud.cn/raw/f3fa3d97e385d113faf053cb989edef7.png)

## Strengths of Kerberos Authentication for GooseFS

- The authentication architecture and process are basically the same as those of HDFS connection to Kerberos. Applications for which the Kerberos authentication process is enabled in HDFS can be migrated to GooseFS easily.
- The Hadoop Delegation Token authentication mechanism is supported, so GooseFS is well compatible with Hadoop-based application jobs.

## Configuring GooseFS connection to Kerberos

### Prerequisites

- GooseFS 1.3.0 or later.
- Make sure that the Kerberos KDC service exists in your environment and GooseFS and the application client can access its port normally.

### Creating the GooseFS identity information in Kerberos KDC

First, create Kerberos identities for the GooseFS cluster server and client in Kerberos KDC before configuring the connection. Here, `kadmin.local` is used on the **Kerberos KDC server** for creation:
>! You need to run the `kadmin.local` tool with the `root/sudo` privileges.
>

```shell
$ sudo kadmin.local
```

If the command is executed successfully, you will enter the interactive shell environment of kadmin:

```shell
Authenticating as principal root/admin@GOOSEFS.COM with password.
kadmin.local:  
```

Here, `kadmin.local` indicates the command prompt of the interactive execution environment.

#### Creating GooseFS server/client identities

The following takes a simple test cluster and its use case as an example to describe how to configure Kerberos:
1. Cluster environment description:
A one-master-dual-worker standalone architecture is used:
 - Master (JobMaster): 172.16.0.1
 - Worker 1 (JobWorker1): 172.16.0.2
 - Worker 2 (JobWorker2): 172.16.0.3
 - Client: 172.16.0.4
2. Create the server and client identities in `kadmin.local`:
```shell
kadmin.local: addprinc -randkey goosefs/172.16.0.1@GOOSEFS.COM
kadmin.local: addprinc -randkey client/172.16.0.4@GOOSEFS.COM
```
>! Here, `-randkey` is used as no matter whether you log in to GooseFS on the server or client, a `.keytab` file instead of a plaintext password will be used for authentication. If the identity information needs to be used for login with a password, you can remove this field.
>
3. Generate and export the `.keytab` file for each identity:
```shell
kadmin.local: xst -k goosefs_172_16_0_1.keytab goosefs/172.16.0.1@GOOSEFS.COM
kadmin.local: xst -k client_172_16_0_4.keytab client/172.16.0.4@GOOSEFS.COM
```

### Configuring Kerberos authentication for GooseFS server/client access

1. Distribute the `.keytab` files exported above to the corresponding servers. Here, we recommend you use the path `${GOOSEFS_HOME}/conf/`.
```shell
$ scp goosefs_172_16_0_1.keytab <username>@172.16.0.1:${GOOSEFS_HOME}/conf/
$ scp goosefs_172_16_0_1.keytab <username>@172.16.0.2:${GOOSEFS_HOME}/conf/
$ scp goosefs_172_16_0_1.keytab <username>@172.16.0.3:${GOOSEFS_HOME}/conf/
$ scp client_172_16_0_4.keytab <username>@172.16.0.4:${HOME}/.goosefs/
```
2. On the corresponding server, change the user/user group to which the server principal keytab file belongs to the user/user group used during GooseFS server startup, so as to grant GooseFS the required read permission during startup.
```shell
$ chown <GooseFS_USER>:<GOOSEFS_USERGROUP> goosefs_172_16_0_1.keytab
$ # Modify the Unix access permission bit
$ chmod 0440 goosefs_172_16_0_1.keytab
```
3. Change the user/user group to which the client keytab file belongs to the client account initiating GooseFS requests, so as to guarantee that the client has the required permission to read the file.
```shell
$ chown <client_user>:<client_usergroup> client_172_16_0_4.keytab
$ # Modify the Unix access permission bit
$ chmod 0440 client_172_16_0_4.keytab
```

#### GooseFS configuration on the server and client

1. `goosefs-site.properties` on the master/worker server:
```properties

# Security properties
# Kerberos properties
goosefs.security.authorization.permission.enabled=true
goosefs.security.authentication.type=KERBEROS
goosefs.security.kerberos.unified.instance.name=172.16.0.1
goosefs.security.kerberos.server.principal=goosefs/172.16.0.1@GOOSEFS.COM
goosefs.security.kerberos.server.keytab.file=${GOOSEFS_HOME}/conf/goosefs_172_16_0_1.keytab

```
After configuring authentication on the GooseFS server, restart the entire cluster for the configuration to take effect.
2. `goosefs-site.properties` on the client:
```properties
# Security properties
# Kerberos properties
goosefs.security.authorization.permission.enabled=true
goosefs.security.authentication.type=KERBEROS
goosefs.security.kerberos.unified.instance.name=172.16.0.1
goosefs.security.kerberos.server.principal=goosefs/172.16.0.1@GOOSEFS.COM
goosefs.security.kerberos.client.principal=client/172.16.0.4@GOOSEFS.COM
goosefs.security.kerberos.client.keytab.file=${GOOSEFS_HOME}/conf/client_172_16_0_4.keytab

```
>! You need to specify the server principal on the client, as in the Kerberos authentication system, KDC needs to know the service accessed by the client currently, and GooseFS uses the server principal to identify the service requested by the client currently.
>

At this point, GooseFS has been connected to the basic authentication service of Kerberos, and all requests initiated by the client will be authenticated by Kerberos subsequently.

