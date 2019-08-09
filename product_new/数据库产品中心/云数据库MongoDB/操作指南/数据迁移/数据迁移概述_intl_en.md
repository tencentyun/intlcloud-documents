## How to Use MongoDB Migration Tool
## Overview of Client's Instance Migration
TencentDB for MongoDB supports two types of migration: client's CVM instance migration and public network instance migration.
#### Glossary

| Term | Description |
|---------|---------|
| Source instance | Source instance of the migration |
| Target instance | Target instance of the migration, i.e. TencentDB for MongoDB instance purchased by the user |
| Server | The server in which the source instance of the migration resides |

#### Notes on Migration
1. To ensure migration efficiency, cross-region migration is not supported for client's CVM instances.
2. For the migration of public network instances, make sure the source instance service is accessible in public networks.
3. After successful migration, you can disconnect from the source instance and switch the connection to the target instance after the data is verified by the application.
4. [Note]: If client's instance has one node, online migration is not supported because a single node has no oplog.

## Migration Process
#### Create a migration task
Enter the "Migration Task List" and create a migration task by following the steps below:
1.	Select the region to which the target instance belongs.
2.	Click **New Instance Migration Task** to open the migration task creation page.

#### Enter basic information
The following description is based on MongoDB instance on CVM. The same is applicable to the public network instance migration.

| Field | Description | Use | Required |
|---------|---------|---------|---------|
| Task name | Name of the migration task | For task management | Yes |
| CVM ID | ID of the Tencent CVM in which the source MongoDB instance resides | Used for checking The migration status of the CVM.  Optional for public network instance migration. | Yes |
| MongoDB IP | Private IP of the Tencent CVM in which the source MongoDB instance resides | Used for checking the private IP of the CVM. | Yes |
| Port | Port number of source instance | The migration task will access the source instance service. | Yes |
| Password | Source instance password |  Used for source instance access authentication. | Yes |
| Target database-instance | Target instance ID | Used for data synchronization. | Yes |


#### Specify the object to migrate
1. Database-level migration is supported. Specify the databases to migrate, and click **Save** to create a task.

2. After a task is successfully created, you can see it on the task list.

#### Start the migration task
1. After the task is created, it is still in "Not Started" status until you click **Start**. The task will begins and verify the parameters.

2. The migration will not be implemented until the parameters are verified.

Note: If the network is inaccessible, please check the security group of the source instance. All ports for the security group should be opened to Internet.

#### Migration process
Click **Start** in the pop-up box to start the migration.
The migration has 3 steps:
1. Data synchronization
2. Index creation
3. oplog synchronization

#### Disconnect synchronization
After all data in the oplog is read and written to the target instance, click **Complete Task** and then **OK** to complete oplog synchronization, and the task will be marked as successful. (You can disconnect the synchronization once you verify the data in the target instance.)
If you want to stop task in the middle of migration, you can click **Stop Task**, and then all the synced operations will be rolled back, and the task will be marked as failed.

