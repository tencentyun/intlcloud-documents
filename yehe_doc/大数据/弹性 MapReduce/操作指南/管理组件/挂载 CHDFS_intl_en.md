## Operation Scenarios
CHDFS is a high-performance distributed file system with standard HDFS access protocols and hierarchical namespaces. EMR supports read/write of data in CHDFS. This document describes how to mount a CHDFS instance to an EMR cluster.

## Directions
### Scenario 1. Mounting a CHDFS instance to a new cluster
>?New cluster: this refers to clusters created on or after December 31, 2019. For new clusters, the default CHDFS mounting address of EMR is `/data/emr/hdfs/tmp/chdfs`.

An EMR cluster is automatically adaptive to CHDFS. Create a CHDFS instance and set permissions reasonably to interconnect the CHDFS instance and EMR cluster. The configuration steps are as follows:
1. Create a CHDFS instance in the same region as the EMR cluster.
2. Create a permission group as needed.
3. Create a permission rule as needed.
4. Create a mount point on the same network as the EMR cluster.
5. Check the connectivity between the CHDFS instance and the EMR cluster. Use the `hadoop fs` command line tool to run the `hadoop fs –ls ofs://${mountpoint}/` command. Here, `mountpoint` is the mounting address. If the file list is output properly, the CHDFS has been successfully mounted.

