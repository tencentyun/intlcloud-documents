TencentDB for MariaDB supports assigning instances to different projects for management.
Project is a resource assignment method defined by Tencent Cloud for teams. You can assign different resources to different teams based on your organizational structure, and this assignment method is called project in Tencent Cloud.

- Read-only replicas and disaster recovery instances are the associated instances of the primary instance and should be in the same project as the primary instance.
- Assigning and moving database instances across projects will not affect the services provided by the instances.
- Users need to specify projects to which the instances belong when purchasing them. The default project is "Default Project".
- Assigned instances can be reassigned to other projects through the **Switch to another project** feature in the [console](https://console.cloud.tencent.com/mariadb).

![](https://main.qcloudimg.com/raw/8ac84456ebfb6debfa1434342941008c.png)
