TencentDB for MySQL supports assigning instances to different projects for management. Notes for assignment are listed below:
- Read-only replicas are the associated instances of the source instance and should be in the same project as the source instance.
- Assigning and reassigning TencentDB instances will not affect the services provided by the instances.
- Users need to specify projects to which the instances belong when purchasing them. The default project is "Default Project".
- Assigned instances can be reassigned to other projects through the **Assign to Project** feature.

## Directions
1. Log in to the [MySQL console](https://console.cloud.tencent.com/cdb/), select an instance, and click **More** > **Assign to Project** at the top of the instance list.

   ![](https://main.qcloudimg.com/raw/d1fe0ad3b002172fbb6418cc8ba830d5.png)

2. In the pop-up dialog box, select a project and click **OK**.
  ![](https://main.qcloudimg.com/raw/f547428bb9ae2fc0d2d8105cff950b85.png)
