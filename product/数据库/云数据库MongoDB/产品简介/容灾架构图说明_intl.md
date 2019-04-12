TencentDB for MongoDB adopts master/slave hot backup architecture. When the master node fails, the service will automatically switch to a slave node. Since a 10-second disconnection may occur during the master/slave switch, you need to set up the auto-restart. The following illustrates how auto disaster recovery works:
1. When the master node is unavailable due to an accident, the system will automatically select an alternative master node in the cluster.
2. If the master node fails, it will become a slave node after the restart. However, if the restart fails, a new node will be added to the cluster to maintain the specified cluster size.
3. Similarly, when a slave node is unavailable, the system will attempt to restart the node or add a new one. <br>

![](https://mc.qcloudimg.com/static/img/5cdada2069c890c3ba44486641413d20/zidongrongzai.png)

