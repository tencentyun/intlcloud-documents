This document describes how to migrate data when removing core nodes tservers from a Kudu cluster.
>? Core nodes can be removed from a Kudu cluster. This feature is not available by default. If you need to use it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

Before disconnecting tservers, you can use the rebalancing tool for data migration. Note that you can disconnect only one tserver at a time. To disconnect multiple ones, repeat the following steps.

## Kudu migration based on rebalancing tool
1. Make sure that the cluster status is **OK**.
```
/usr/local/service/kudu/bin/kudu cluster ksck 10.0.1.29:7051,10.0.1.16:7051,10.0.1.36:7051
```
![](https://qcloudimg.tencent-cloud.cn/raw/5c363c32fd1b5a56ae5c0a2b76798aae.png)
2. Run the `ksck` command in step 1 to get the `uid` of the disconnected nodes.
![](https://qcloudimg.tencent-cloud.cn/raw/3e2bfb44bf57f6a22a615d6bd6a06915.png)
Take the `fb9afb1b2989456cac5800bf6990dfea` node as an example.
3. Switch the `fb9afb1b2989456cac5800bf6990dfea` node to the maintenance mode.
```
/usr/local/service/kudu/bin/kudu tserver state enter_maintenance 10.0.1.29:7051,10.0.1.16:7051,10.0.1.36:7051 fb9afb1b2989456cac5800bf6990dfea
```
4. Run the following `rebalance` command.
```
/usr/local/service/kudu/bin/kudu cluster rebalance 10.0.1.29:7051,10.0.1.16:7051,10.0.1.36:7051 --ignored_tservers fb9afb1b2989456cac5800bf6990dfea --move_replicas_from_ignored_tservers
```
After the command is executed, run the `ksck` command again to check whether the status is **OK** before proceeding.
5. Suspend the tserver process at `10.0.1.45` on the `fb9afb1b2989456cac5800bf6990dfea` node. Note that at this point, if you run the `ksck` command, you will see that the cluster is unhealthy, and you need to restart the tmasters.
![](https://qcloudimg.tencent-cloud.cn/raw/48475acf8c1c4a790bfd52a8c353776a.png)
6. Restart the masters in the [EMR console](https://console.cloud.tencent.com/emr) one by one (rolling restart in the console is not recommended). Then, run the `ksck` command to check whether the cluster is healthy.
![](https://qcloudimg.tencent-cloud.cn/raw/dba5c4af3faac4ca372b1ef34c2e2eb1.png)
