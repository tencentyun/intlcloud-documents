TencentDB for MongoDB uses a master/slave hot backup architecture, where the master node that fails can switch to a slave node. Since a 10-second disconnection may occur during the master/slave switch, auto retry must be set. Auto disaster recovery works in the following way:
1. When the master node is unreachable due to an accident, a new master node will be selected automatically within the cluster.
2. If the master node fails, it will become a slave node after it restarts. If it fails to restart, a new node will be added to the cluster to reach the size selected by a user.
3. When a slave node is unreachable, the system will attempt to start the node or add a new one.
![](https://mc.qcloudimg.com/static/img/5cdada2069c890c3ba44486641413d20/zidongrongzai.png)

