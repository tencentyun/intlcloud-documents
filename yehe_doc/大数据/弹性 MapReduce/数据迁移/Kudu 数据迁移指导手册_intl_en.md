Kudu can use the rebalancing tool to migrate data.
>!You can disconnect only one tserver at a time. To disconnect multiple ones, repeat the following steps.

## Kudu Migration Based on Rebalancing Tool
1. Make sure that the cluster status is **OK**.
```
 /usr/local/service/kudu/bin/kudu cluster ksck 10.0.1.29:7051,10.0.1.16:7051,10.0.1.36:7051
```
![](https://qcloudimg.tencent-cloud.cn/raw/7b11bf98171f44cd24bc671194fa313b.png)  

2. Run the ksck command as described in step 1 to get the `uid` of the disconnected nodes. 
![](https://qcloudimg.tencent-cloud.cn/raw/82caa032beaaa649683f80e22fd8083f.png)
Take the `fb9afb1b2989456cac5800bf6990dfea` node as an example.

3. Switch the `fb9afb1b2989456cac5800bf6990dfea` node to the maintenance mode.
```
 /usr/local/service/kudu/bin/kudu tserver state enter_maintenance 10.0.1.29:7051,10.0.1.16:7051,10.0.1.36:7051 fb9afb1b2989456cac5800bf6990dfea
```

4. Run the following rebalancing command.
```
 /usr/local/service/kudu/bin/kudu cluster rebalance 10.0.1.29:7051,10.0.1.16:7051,10.0.1.36:7051 --ignored_tservers fb9afb1b2989456cac5800bf6990dfea --move_replicas_from_ignored_tservers
```
After the command is executed, run the ksck command again to check whether the status is **OK** before proceeding.

5. Suspend the tserver process at `10.0.1.45` on the `fb9afb1b2989456cac5800bf6990dfea` node. Note that at this point, if you run the ksck command, you will see that the cluster is unhealthy, and you need to restart the tmasters. 
![](https://qcloudimg.tencent-cloud.cn/raw/216ee22e20f45c4ca26143dd115c694f.png)
6. Restart the masters in the EMR console one by one (rolling restart in the console is not recommended). Then, run the ksck command to check whether the cluster is healthy.
![](https://qcloudimg.tencent-cloud.cn/raw/e01de51289a885adb262bcc81803623e.png)
