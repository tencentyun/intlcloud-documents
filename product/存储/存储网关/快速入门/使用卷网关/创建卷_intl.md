After a volume gateway is created, you need to allocate the cloud storage space for the gateway to store user-uploaded data.
On the "CSG Console - Gateway" page or "Volume" page, click **Create a Volume**. Enter corresponding information in the pop-up.

* Region: Select the region where the gateway is located.
* Gateway: Select the gateway to which to add the volume. After creation, this cannot be modified.
* Volume name: The volume name is part of the iSCSI Target name. It must be globally unique for one single user and contain 1-16 English letters or digits.
* iSCSI Target: The first half is in a fixed format (iqn.2003-07.com.qcloud), and the **volume name** is what you enter in the field above.
* Volume content: You need to specify whether this is to create an empty volume or restore previous data (by selecting "Based on snapshot"; if you do so, you can select the snapshot you want to restore in the snapshot list).
* Volume capacity: Set the capacity of the volume. If you are creating a volume based on a snapshot, the volume capacity must be greater than or equal to the capacity of the snapshot.

 ![](https://mc.qcloudimg.com/static/img/f5fd35f6707eec30678ad2179b79e44a/image.png)   

