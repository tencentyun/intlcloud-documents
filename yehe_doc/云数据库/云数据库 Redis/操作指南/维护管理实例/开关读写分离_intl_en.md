## Operation Scenarios
TencentDB for Redis supports [read/write separation](https://intl.cloud.tencent.com/document/product/239/33132) for business scenarios with more reads but less writes, which can well cope with read requests concentrating on frequently read data. It supports up to 1-master 5-slave mode to offer 5x read performance.
>!
>- Enabling read/write separation may cause data read inconsistency (the data on replica nodes are older than that on the master node). Please check whether your business can tolerate data inconsistency first.
>- Disabling read/write separation may interrupt existing connections momentarily, so you are recommended to do so during off-peak hours.

## Directions
1.Log in to the [Redis Console](https://console.cloud.tencent.com/redis) and click an instance ID in the instance list to enter the instance management page.
2. Select the **Node Management** tab and click **Read-Only Replica** to enable read/write separation.
![](https://main.qcloudimg.com/raw/1d66625e3868fa6850648bd1737f7435.png)
3. In the pop-up dialog box, confirm that everything is correct and click **OK**.

