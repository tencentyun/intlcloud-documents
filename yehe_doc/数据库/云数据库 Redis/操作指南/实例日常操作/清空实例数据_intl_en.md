## Overview

TencentDB for Redis supports quickly clearing all instance data in the console. Clearing an instance will perform the **FLUSHALL** operation on the instance, and all instance data will be cleared and cannot be recovered. Proceed with caution.

## Notes

- Once cleared, the data cannot be recovered. Make sure you have backed up all data before submitting a clearing request.
- Data clearing will affect the service provided by the instance, and the instance cannot be accessed during the clearing process.
- When a master instance in a global replication group is cleared up, all of the other instances in the group are cleared up as well.
- In a global replication group, you can't clear up a read-only instance as clearup is a write operation. You can clear up the group after removing all read-only instances from it.

## Directions

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Click the target instance ID to enter the **Instance Details** page.
5. In the top-right corner of the **Instance Details** page, click **Clear Instance**.
![](https://qcloudimg.tencent-cloud.cn/raw/b2d3d24e3449235b2c826728d55c6cee.png)
6. In the **Clear Instance** dialog box, learn about the impact of instance clearing, enter the instance access password in the input box next to **Password**, and click **OK**.
>?The password to be entered here is the instance password you set rather than the connection password in the format of "instance ID:instance password" used for instance access.
7. On the left sidebar, select **Task Management** and wait for the task to complete.

## Related APIs

| API | Description      |
| :----------------------------------------------------------- | :------------ |
| [ClearInstance](https://intl.cloud.tencent.com/document/product/239/32070) | Clears a Redis instance. |

