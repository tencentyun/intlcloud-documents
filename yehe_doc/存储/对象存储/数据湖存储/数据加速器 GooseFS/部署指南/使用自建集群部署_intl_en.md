This document describes how to deploy, configure, and run GooseFS on a single server, in a cluster, and in the Tencent Cloud EMR cluster that has not integrated with GooseFS.

## Environment Requirements

### Hardware environments

Currently, GooseFS can work with Linux/MacOS running a mainstream x86/x64 framework (**Note: M1-powered MacOS has not been verified**). Configuration requirements for nodes are described as follows:

#### Master nodes

- **CPU**: A clock rate of 1 GHz or above. Since the master node needs to process a large amount of data, we recommend you use multi-core processors in the production environment.
- **Physical memory**: 1 GB or above. We recommend you use at least 8 GB of physical memory in the production environment.
- **Disk**: 20 GB or above. We recommend you use high-performance NVME SSD as the metadata caching disk (RocksDB mode) in the production environment.

#### Worker nodes

- **CPU**: A clock rate of 1 GHz or above. Since a worker node also needs to handle a lot of concurrent requests, we recommend you use multi-core processors in the production environment.
- **Physical memory**: 2 GB or above. You can allocate memory for the production environment according to your performance needs. For example, if you need to cache a lot of data blocks to the worker node memory, or use mixed storage (MEM + SSD/HDD), you can allocate the physical memory according to the volume of data that might be cached to the memory. We recommend you use at least 16 GB of physical memory for workers in the production environment, regardless of what caching mode you use.
- **Disk**: An SSD/HDD disk of at least 20 GB. We recommend you allocate disk space for each worker node by estimating the amount of data that might need to be cached to the production environment. Moreover, for better performance, we recommend you use NVME SSD disks for worker nodes.

### Software environments

- Red Hat Enterprise Linux 5.5 or later, Ubuntu Linux 12.04 LTS or later (supported if batch deployment is not used), CentOS 7.4 or later, TLinux 2.x (Tencent Linux 2.x), and Intel-based MacOS 10.8.3 or later. If you use Tencent Cloud CVM, we recommend you use CentOS 7.4, Tencent (TLinux 2.x), or TencentOS Server 2.4.
- OpenJDK 1.8/Oracle JDK 1.8. Note that JDK 1.9 or later versions have not been verified.
- Supports SSH tools (including SSH and SCP tools), Expect Shell (for batch deployment), and Yum Package Manager.

### Cluster network environments

- Master and worker nodes need to be connected via a public/private network. If batch deployment is used, the master node needs to be able to access the public software source properly, or can correctly configure private software sources in the package management system.
- The cluster can access COS buckets or CHDFS over a public/private network.

### Security group and permission requirements

In most cases, you are advised to use a dedicated Linux account to deploy and run GooseFS. For example, in the self-built cluster and EMR environment, you can use the Hadoop user to deploy and run GooseFS. If batch deployment is used, the following permissions are also needed:

- Permission to switch to the root account or use `sudo`.
- The running and deployment account needs to have permission to read and write to the installation directory.
- The master node should have permission to use SSH to log in to all worker nodes in the cluster.
- The corresponding node role in the cluster should open the corresponding port(s) (master: 9200 and 9201; worker: 9203 and 9204; job master: 9205, 9206, and 9207; job worker: 9208, 9209, and 9210; proxy: 9211; LogServer: 9212).

## Single-Server Deployment and Running (Pseudo-Distribution Framework)

The pseudo–distribution framework is mainly used for trying out and debugging GooseFS. Beginners can try out and debug GooseFS on a host running Linux OS or macOS.

### Deployment

1. [Download the GooseFS binary distribution package](https://downloads.tencentgoosefs.cn/goosefs/1.4.1/release/goosefs-1.4.1-bin.tar.gz)).
2. Decompress the package, go to the GooseFS directory, and perform the operations below.
- Create the `conf/goosefs-site.properties` configuration file by copying `conf/goosefs-site.properties.template`.
```bash
 $ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```
- Set `goosefs.master.hostname` to `localhost` in `conf/goosefs-site.properties`.
- In `conf/goosefs-site.properties`, set `goosefs.master.mount.table.root.ufs` to the directory in the local file system, such as `/tmp` or `/data/goosefs`.

You are advised to set SSH passwordless login for localhost. Otherwise, you need to enter its login password for operations such as formatting and starting.

### Running

Run the following command to mount a RamFS file system:

```bash
$ ./bin/goosefs-mount.sh SudoMount
```

You can also mount it directly when you start the GooseFS cluster as follows:

```bash
$ ./bin/goosefs-start.sh local SudoMount
```

When the cluster is started, run the `jps` command to view all GooseFS processes in the pseudo-distribution mode.

```bash
$ jps
35990 Jps
35832 GooseFSSecondaryMaster
35736 GooseFSMaster
35881 GooseFSWorker
35834 GooseFSJobMaster
35883 GooseFSJobWorker
35885 GooseFSProxy
```

After this, you can run the `goosefs` command to perform operations related to namespace, fileSystem, job, and table. For example, you can run the following commands to upload a local file to GooseFS and list files and directories in the root directory of GooseFS:

```bash
$ goosefs fs copyFromLocal test.txt /
Copied file:///Users/goosefs/test.txt to /

$ goosefs fs ls /
-rw-r--r--  goosefs         staff                        0       PERSISTED 04-28-2021 04:00:35:156 100% /test.txt

```

The GooseFS CLI tool allows you to perform all kinds of operations on namespaces, tables, jobs, file systems, and more to manage and access GooseFS. For more information, please see our documentation or run the `goosefs -h` command to view the help messages.

## Cluster Deployment and Running

The cluster deployment and running are mainly for the production environment of self-built IDC clusters and Tencent Cloud EMR production environments that have not integrated with GooseFS. The deployments are classified into standalone framework deployment and high-availability (HA) framework deployment.

In the `scripts` directory, you can find scripts to configure SSH passwordless logins or deploy GooseFS in batches, which make it easy to deploy a large-scale GooseFS cluster. See the batch deployment requirements mentioned above to check whether you can use batch deployment.

### Introduction to the batch deployment tool

GooseFS provides scripts in the `scripts` directory for you to configure SSH passwordless logins or deploy GooseFS in batches. If the execution conditions are met, you can perform the following steps to batch deploy jobs:
- Enter the extracted GooseFS directory by running `cd ${GOOSEFS_HOME}`.
- Configure the hostname or IP address in `conf/masters` and `conf/workers`.
- Go to the `scripts` directory and configure the `SCRIPT_EXEC_USER` and `SCRIPT_EXEC_PASSWORD` carefully in the `commons.sh` script file. Then, switch to the `root` account or use `sudo` to run `config_ssh.sh`, so that you can configure passwordless logins for the entire cluster.
- Run the `validate_env.sh` tool to validate the configuration of the cluster.
- Create a soft link to the configuration file directory by running `ln -s conf ~/.goosefs`.
- Finally, run `goosefs copy .` and `goosefs copy ~/.goosefs` to distribute the GooseFS binary package and configuration file to all nodes.

After a successful deployment, run `./bin/goosefs-start.sh all SudoMount` to start the entire cluster. By default, all running logs will be recorded to `${GOOSEFS_HOME}/logs`.

### Standalone framework deployment

In the standalone framework, only one master node and multiple worker nodes are deployed in the cluster. You can deploy and run the cluster as follows:

1. [Download the GooseFS binary distribution package](https://downloads.tencentgoosefs.cn/goosefs/1.4.1/release/goosefs-1.4.1-bin.tar.gz)).
2. Run the `tar zxvf goosefs-x.x.x-bin.tar.gz` command to decompress the package into the installation directory. You can see **Introduction to the batch deployment tool** to deploy and run your cluster in batches, or perform the following steps to deploy it manually.

(1) Copy the `template` file from the `conf` directory to create a configuration file.
```bash
$ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```
(2) Configure `goosefs-site.properties` as follows:
```properties
goosefs.master.hostname=<MASTER_HOSTNAME>
goosefs.master.mount.table.root.ufs=<STORAGE_URI>
```
Set `goosefs.master.hostname` to the hostname or IP of the master node, and `goosefs.master.mount.table.root.ufs` to the URI in the under file system (UFS) to which the GooseFS root directory is mounted. 
>!This URI must be accessible for both the master and worker nodes and therefore it cannot be a local directory.

For example, you can mount a COS path to the root directory of GooseFS with `goosefs.master.mount.table.root.ufs=cosn://bucket-1250000000/goosefs/`.

In the `masters` configuration file, specify the hostname or IP of the master node as follows:

```plaintext
# The multi-master Zookeeper HA mode requires that all the masters can access
# the same journal through a shared medium (e.g. HDFS or NFS).
# localhost
cvm1.compute-1.myqcloud.com
```

In the `workers` configuration file, specify the hostname or IP for all worker nodes as follows:

```plaintext
# An GooseFS Worker will be started on each of the machines listed below.
# localhost
cvm2.compute-2.myqcloud.com
cvm3.compute-3.myqcloud.com
```

After the configuration is completed, run `./bin/goosefs copyDir conf/` to sync the configurations to all nodes.

Finally, run `./bin/goosefs-start.sh all` to start the GooseFS cluster.


### HA framework deployment

The standalone framework that uses only one master node might lead to a single point of failure (SPOF). Therefore, you are advised to deploy multiple master nodes in the production environment to adopt an HA framework. One of the master nodes will become the leader node that provides services, while other standby nodes will share journals synchronously to maintain the same state as the leader node. If the leader node fails, one of the standby nodes will automatically replace the leader node to continue providing services. In this way, you can avoid SPOFs and make the framework more highly available.

Currently, GooseFS supports using Raft logs or ZooKeeper to ensure the strong consistency of the leader and standby nodes. The deployment of each mode is described below.

#### HA framework based on Raft embedded logs

First, create a configuration file using a template.

```bash
$ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```

```properties
goosefs.master.mount.table.root.ufs=<STORAGE_URI>
goosefs.master.embedded.journal.addresses=<EMBBEDDED_JOURNAL_ADDRESS>
```

>? The configuration items are described as follows:
-  Set `goosefs.master.mount.table.root.ufs` to the underlying storage URI that is mounted to the GooseFS root directory.
-  Set `goosefs.master.embedded.journal.addresses` to the `ip:embedded_journal_port` or `host:embedded_journal_port` of all standby nodes. The default value of `embedded_journal_port` is 9202. For example, `goosefs.master.embedded.journal.addresses` can be set to 192.168.1.1:9202, 192.168.1.2:9202, and 192.168.1.3:9202. 

The deployment based on Raft embedded logs uses [copycat](https://github.com/atomix/copycat) to select a leader node. Therefore, if you use Raft for an HA framework, do not mix it with ZooKeeper.

After the configurations are completed, run the following command to sync all configurations:

```bash
$ ./bin/goosefs copyDir conf/
```

Format and then start the GooseFS cluster:

```bash
$ ./bin/goosefs format
```

```bash
$ ./bin/goosefs-start.sh all
```
If the system prompts that you don't have the permission, restart as follows:
```bash
$ ./bin/goosefs-stop.sh all
$ ./bin/goosefs-start.sh all SudoMount
```

Run the following command to view the current leader node:

```bash
$ ./bin/goosefs fs leader
```

Run the following command to view the cluster status:

```bash
$ ./bin/goosefs fsadmin report
```

#### Deployment based on ZooKeeper and shared logs

To set up an HA GooseFS framework based on ZooKeeper, you need to:
 - Have a ZooKeeper cluster. GooseFS uses ZooKeeper to select the leader node, and the client and worker nodes use ZooKeeper to query the leader node.
 - Have a highly available and strongly consistent shared file system, which must be accessible for all GooseFS master nodes. The leader will write the logs to the file system, and standby nodes will read logs from the file system constantly and replay logs to ensure state consistency. You are advised to use HDFS or COS (for example, `hdfs://10.0.0.1:9000/goosefs/journal` or `cosn://bucket-1250000000/journal`) as the shared file system.

The configurations are as follows:

```properties
goosefs.zookeeper.enabled=true
goosefs.zookeeper.address=<ZOOKEEPER_ADDRESSS>
goosefs.master.journal.type=UFS
goosefs.master.journal.folder=<JOURNAL_URI>
```

Note that `JOURNAL_URI` in ZK mode must be a URI of the shared storage system. Then, use `./bin/goosefs copyDir conf/` to sync the configurations to all nodes in the cluster, and use `./bin/goosefs-start.sh all` to start the cluster.


## GooseFS Process List

After the `goosefs-start.sh all` script is executed and GooseFS is started, the following processes will run in the cluster:

| Process | Description |
| ---------------- | ----------------------------------- |
|GooseFSMaster   | Default RPC port: 9200; web port: 9201  |
|  GooseFSWorker  | Default RPC port: 9203; web port: 9204   |
|  GooseFSJobMaster    | Default RPC port: 9205; web port: 9206   |
|  GooseFSProxy      |   Default web port: 9211   |
| GooseFSJobWorker   | Default RPC port: 9208; web port: 9210  |

