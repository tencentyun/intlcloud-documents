In Hadoop, distributed file system HDFS, resource scheduling framework YARN, and iterative computing framework MR. Tencent Cloud's Hadoop version that have integrated with COS, allowing you to access to COS by running the `hadoop fs` command line so as to separate compute and storage apart. Below are some best practices:
1. HDFS  
For both high-availability (HA) cluster and non-HA cluster, **do not format the namenode**; otherwise, your data will be lost permanently. Tencent Cloud shall not be responsible under any circumstance for any loss of data caused by formatting the namenode.
2. YARN  
The fair scheduler is enabled by default, and you can change the scheduler based on your actual needs.
