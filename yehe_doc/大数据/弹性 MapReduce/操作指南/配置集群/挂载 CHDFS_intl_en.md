## Overview
CHDFS is a high-performance distributed file system with standard HDFS access protocols and hierarchical namespaces. EMR supports read/write of data in CHDFS. This document describes how to mount a CHDFS instance to an EMR cluster.

## Directions

### Scenario 1. Mounting a CHDFS instance to a new cluster
>? New cluster: This refers to clusters created on or after December 31, 2019. For new clusters, the default CHDFS mounting address of EMR is `/data/emr/hdfs/tmp/chdfs`.

An EMR cluster is automatically adaptive to CHDFS. Create a CHDFS instance and set permissions reasonably to interconnect the CHDFS instance and EMR cluster. The configuration steps are as follows:
1. Create a CHDFS instance in the same region as the EMR cluster as instructed in [Creating CHDFS Instance](https://intl.cloud.tencent.com/document/product/1106/41961).
2. Create a permission group as needed as instructed in [Creating Permission Group](https://intl.cloud.tencent.com/document/product/1106/41962).
3. Create permission rules as needed as instructed in [Creating Permission Rule](https://intl.cloud.tencent.com/document/product/1106/41963).
4. Create a mount point on the same network as the EMR cluster as instructed in [Creating Mount Point](https://intl.cloud.tencent.com/document/product/1106/41964).
5. Check the connectivity between the CHDFS instance and the EMR cluster. Use the `hadoop fs` command line tool to run the `hadoop fs –ls ofs://${mountpoint}/` command. Here, `mountpoint` is the mounting address. If the file list is output properly, the CHDFS has been successfully mounted.

### Scenario 2. Mounting a CHDFS instance to a legacy cluster
>? Legacy cluster: This refers to clusters created before December 31, 2019. 

For more information on how to mount a CHDFS instance to a legacy EMR cluster, see [Mounting CHDFS Instance](https://intl.cloud.tencent.com/document/product/1106/41965).
