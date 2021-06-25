## Overview
TencentDB for Redis supports disabling some commands that may cause service instability or accidentally delete data.

You can configure the `disable-command-list` parameter to disable such commands. If this parameter is not displayed in your console, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to upgrade the minor kernel version. A short disconnection will occur during the version upgrade, and you can reconnect after the upgrade is completed.

## Directions
### Disabling a command
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. Select **Parameter Configuration** > **Modifiable Parameters** and configure the list of commands to be disabled in the `disable-command-list` parameter line.
>?
>- Commands that can be disabled include `flushall`, `flushdb`, `keys`, `hgetall`, `eval`, `evalsha`, and `script`, which are not disabled by default on new TencentDB for Redis instances purchased after January 1, 2019.
>- Command disablement will take effect within two minutes for existing connections without restarting the Redis service.
>
![](https://main.qcloudimg.com/raw/3641b6811d698955f9564a34dfe73e36.png)

### Enabling a disabled command
On the **Parameter Configuration** > **Modifiable Parameters** tab, remove a command from the list of disabled commands in **Current Value** to enable it.

### Parameter modification history
View the parameter modification history on the **Parameter Configuration** > **Modification Log** tab.

