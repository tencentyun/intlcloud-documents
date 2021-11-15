
TencentDB for Redis is compatible with Redis 2.8, 4.0, and 5.0. Upgrade to a compatible version is supported, so that you can upgrade your instance to a newer version for more features.

## Upgrade Description
- Currently, only standard architecture instances can be upgraded to a compatible version.
- Instances can be upgraded from a lower version to a higher one; for example, you can upgrade from Redis 2.8 to 4.0 or from 4.0 to 5.0.
- Cross-version upgrade is supported; for example, you can upgrade from Redis 2.8 to 5.0.
- If an instance is upgraded to a compatible version, no billing changes will be caused.
- Downgrade to a compatible version is not supported.

## How Upgrade Works
1. Apply for resources: apply for the resources of the new instance version, including proxy, Redis master node, and Redis replica node resources.
2. Sync the data: sync the full and incremental data from the instance on the old version to the instance on the new version.
3. Wait for the switch: wait until data sync is completed or wait for a switch window.
4. Switch the instances: when the switch conditions are met (data sync is almost completed, and the requirements for the switch window are met), stop writing data into the old instance, unbind the virtual IP (VIP) address from it, and bind the VIP to the new instance.
5. Complete the upgrade: update the instance status.

## Upgrade Impact
The version upgrade process mainly consists of data sync and instance switch:
- During data sync, the service will not be affected.
- During switch, the instances will become read-only for less than 1 minute (to wait for the data sync completion), and a momentary disconnection (within seconds) will occur; therefore, your business should have an automatic reconnection mechanism.

## Upgrade Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), select an region at the top of the instance list, click an instance ID/name, and enter the instance management page.
2. On the instance details page, click **Version Upgrade**.
![](https://main.qcloudimg.com/raw/ebc4ecc50af95d99be2fa23f45d11278.png)
3. In the pop-up dialog box, select the version and switch time and click **OK**.
Switch refers to the process where the new instance replaces the old one. The upgrade feature supports **Switch Now** and **Switch Maintenance Window** options.
    - Switch Now: switch will be performed when data sync is almost completed (data left to be synced is less than 10 MB).
    - Switch Maintenance Window: switch will be performed during the instance maintenance window. If the switch conditions cannot be met in the current maintenance window, switch will be attempted in the next window. You can modify the maintenance time in "Maintenance Window" on the instance details page.
![](https://main.qcloudimg.com/raw/f584ccc7b3004feb662e72e8ddcf819a.png)
4. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.
