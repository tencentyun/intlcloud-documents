## Operation Scenarios
Cloud HDFS (CHDFS) is a high-performance distributed file system with standard HDFS access protocols and hierarchical namespaces. EMR supports read/write of data in CHDFS. This document describes how to mount a CHDFS instance to an EMR cluster.

## Directions
### Scenario 1. Mounting a CHDFS instance to a new cluster
>New cluster: this refers to clusters created on or after December 31, 2019. For new clusters, the default CHDFS mounting address of EMR is `/data/emr/chdfs`.

1. Set the connectivity between CHDFS and EMR.
An EMR cluster is automatically adaptive to CHDFS. Create a CHDFS instance and set permissions reasonably to interconnect the CHDFS instance and EMR cluster.
2. Check the connectivity between CHDFS and EMR.
In the EMR cluster, use the `hadoop fs` command line tool to run the `hadoop fs –ls ofs://${mountpoint}/` command. Here, `mountpoint` is the mounting address. If the file list is output properly, the CHDFS has been successfully mounted.



