After a file gateway is created, you can bind the storage space of a bucket in COS to the file gateway as a file system and then read and write the files stored in COS through the NFS protocol provided by the gateway.
On the "CSG Console - Gateway" page or "File Sharing -> File system" page, click **Create a file system** or **Create**.

![](https://mc.qcloudimg.com/static/img/d487be233e18b20b9fea413510408718/image.png)
![](https://mc.qcloudimg.com/static/img/6c29616e877874399601b32839c4ce35/image.png)



Enter corresponding information in the pop-up:

* Select gateway: Select the gateway for which to create the file system. After creation, this cannot be modified.

* Bucket: The buckets in COS in the region where the gateway is located will be listed here. If there is no bucket in the region, please go to the COS Console to create one. **Note: The bucket name is the mounting path of the file system.**

* File protocol: According to the gateway type, the access protocol supported by the file system is automatically displayed as NFS.

* Storage level: Files uploaded via the gateway are stored as "standard" or "low-frequency" type by default. **Note: The shortest storage period of low-frequency storage is 30 days. If it is deleted or modified within less than 30 days, the storage fee will still be charged for 30 days.**

* Allowed accessing address: Set the whitelist of visiting IPs or IP address range to allow these clients to mount and access the file system. If this field is left blank, access is allowed for all clients. In addition, if it is a multi-IP server, please enter the private IP of the server.

* Authorization: As the files stored in COS belong to the user account, only after authorization is granted can the gateway have the permission to access such files when reading and writing them. Specific permissions include those for configuring the bucket, reading, writing and deleting all files in the bucket and managing the bucket lifecycle. (The gateway itself does not initiate any operations to the files in COS. Instead, all operations have to be initiated by user and then executed by the gateway.)

 ![](https://mc.qcloudimg.com/static/img/7f18a4e9f137b7e9433db208112af5e3/image.png) 


