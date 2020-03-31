TencentDB for MariaDB supports assigning instances to different projects for management.
Project is a resource assignment method defined by Tencent Cloud for teams. You can assign different resources to different teams based on your organizational structure, and this assignment method is called project in Tencent Cloud.

- Read-only instances and disaster recovery instances are associated instances of the master instance and should be in the same project as the master instance.
- Assigning and moving database instances across projects will not affect the services provided by the instances.
- You need to specify a project to which a new instance belongs when purchasing it. The default project is **Default Project**.
- Assigned instances can be reassigned to other projects through the **Switch to another project** feature.
![](https://main.qcloudimg.com/raw/bb281d4c40373dbf6e3ee01ac407ba91.png)
