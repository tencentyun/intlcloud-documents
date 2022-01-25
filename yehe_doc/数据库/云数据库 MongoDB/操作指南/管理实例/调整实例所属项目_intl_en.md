TencentDB for MongoDB allows you to assign an instance to a new project in the console to meet your requirements in ever-changing business scenarios.

## Background
A project is a set of applications or services that share resources. Applications, services, and resources in different projects are isolated from and don't affect each other, and each project is unique.

You can specify an appropriate project for your database instances to facilitate collaboration. In this way, you can easily manage your instances globally and stay on top of the operational conditions of the entire project.

## Version Description
Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support instance project adjustment.

## Billing Description
Changing the instance project doesn't incur additional fees.

## Notes
Assigning and reassigning TencentDB instances among projects will not affect the services provided by the instances.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- You have specified a project for the instance. The **Default Project** is used by default.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. In the **Basic Info** section, click **Switch to Another Project** on the right of **Project**.
7. On the **Assign to Project** page, select the target project.
8. Click **OK**. In the **Basic Info** section, <img src="https://qcloudimg.tencent-cloud.cn/raw/a157fe7de2ca05dd886951ce68d993ea.png" style="zoom:65%;" /> will be displayed on the right of **Instance Status**.
9. Wait for the task to be completed. On the right of **Project**, you can see the project to which the instance is reassigned.
You can filter instances by **Project** in the instance list to view the running status of each instance in the entire project.

## API
| API Name                                                  | Feature Description            |
| ------------------------------------------------------------ | -------------------------- |
| [AssignProject](https://intl.cloud.tencent.com/document/product/240/34705) | Specifies the project of TencentDB instance. |


