TencentDB for MySQL supports assigning instances to different projects for management. Notes for assignment are listed below:
- Read-only instances and disaster recovery instances are the associated instances of the source instance and should be in the same project as the source instance.
- Assigning and reassigning TencentDB instances will not affect the services provided by the instances.
- You need to specify a project to which a new instance belongs when purchasing it. **Default Project** will be used if you don't specify one.
- Assigned instances can be reassigned to other projects through the **Assign to Project** feature.

## Assigning the project on the purchase page
1. Log in to the [TencentDB for MySQL purchase page](https://buy.cloud.tencent.com/cdb).
2. When purchasing a new instance, you can directly specify the project to assign the instance to.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Fnk2233_1.png)

## Modifying the project on the purchase page
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. Click **Switch to Another Project** after **Basic Info** > **Project**, select the target project in the pop-up window, and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/GS8u053_2.png)
>?You can also batch assign multiple instances to a project by selecting them and clicking **More** > **Assign to Project** above the instance list.
