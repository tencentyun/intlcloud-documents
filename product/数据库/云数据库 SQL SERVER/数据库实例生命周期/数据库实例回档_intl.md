With the aid of the database rollback capability, system loss can be minimized. Full backups and log backups of TencentDB for SQL Server are retained for **7 days**, so you can roll back to any point in time within the past 7 days.
The specific operation method is as follows:
1.	Go to the instance details page and click the Rollback button.
![](//mccdn.qcloud.com/static/img/6e9523611eb2bb6574c23bb78f2ed3c3/image.png)
2.	Select the database to be rolled back, set the rollback time and whether to overwrite the original database, and then click the Next button.
![](//mccdn.qcloud.com/static/img/71e6e919e84f6c38e396daed4ea1c7fd/image.png)
3.	After confirming the parameters set, click the "Rollback" button to start the rollback task.
![](//mccdn.qcloud.com/static/img/43835ee5e83586111988a40b2c77d346/image.png)
4.	The instance state changes to "task in progress" and you can view the rollback progress in the task list.
![](//mccdn.qcloud.com/static/img/6745a9fe2877d953d07de00cfaade272/image.png)
5.	The rollback task succeeds. As "Overwrite original database" was not selected previously, you can see the generated duplicate database on the database management page.
![](//mccdn.qcloud.com/static/img/5e8c765027e5acea83a52f4b7e8203d2/image.png)
Note: Rollback is currently only supported for local instances, and you can choose to overwrite the original database or generate a duplicate database. If you choose to generate a duplicate database, you need to note that the disk space after rolling back cannot exceed the disk space available for the instance; otherwise, rollback will fail.
