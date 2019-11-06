## Operation Scenarios
Using certain Redis commands may result in service instability or mistaken data deletion; therefore, TencentDB for Redis provides the feature to disable such commands.

TencentDB for Redis 2.8 Standard Edition, 4.0 Standard Edition, and 4.0 Cluster Edition support configuring the `disable-command-list` parameter to disable such commands. If this parameter is not displayed in your console, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to upgrade the backend version. A short disconnection will occur during the version upgrade, and you can simply reconnect after the upgrade is completed.

## Directions
### Disabling a Command
1. Log in to the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis) and click an instance ID/name to enter the instance management page.
2. Select **Parameter Settings** > **Modifiable Parameters** and configure the list of commands to be disabled in the `disable-command-list` parameter line.


>- Commands that can be disabled include flushall, flushdb, keys, hgetall, eval, evalsha, and script, which are not disabled by default on new TencentDB for Redis instances purchased after January 1, 2019.
>- Command disablement will take effect within two minutes for existing links without restarting the Redis service.
>
>![](https://main.qcloudimg.com/raw/3d3b1b62934b2d9bebf81eb4f886c91e.png)

### Enabling a Disabled Command
Select **Parameter Settings** > **Modifiable Parameters** and remove a disabled command from the list of disabled commands in **Current Value** to enable the command.

## Parameter Modification History
You can view the modification history of a parameter in **Parameter Settings** > **Modification Log**.
![](https://main.qcloudimg.com/raw/f3d35543168c0b11dcbb945ee92ad02a.png)
