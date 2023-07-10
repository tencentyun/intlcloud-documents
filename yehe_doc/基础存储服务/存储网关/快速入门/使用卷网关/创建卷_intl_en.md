After a volume gateway is created, you need to allocate the cloud storage capacity for the gateway to store user-uploaded data.
On the "Volume" page in the [CSG Console](https://console.cloud.tencent.com/csg/volume), click **Create Volume**. Enter corresponding information in the pop-up window.

* Region: select the region where the gateway resides.
* Gateway: select the gateway to which to add the volume. After creation, this cannot be modified.
* Volume name: the volume name is part of the iSCSI Target name. It must be globally unique for one single user and contain 1–16 letters or numbers.
* iSCSI Target: the first half is fixed as `iqn.2003-07.com.qcloud`, and the **volume name** is what you enter in the field above.
* Volume content: you need to specify whether this is to create an empty volume or restore previous data (by selecting "Based on snapshot"; if you do so, you can select the snapshot you want to restore in the snapshot list).
* Volume capacity: set the capacity of the volume. If you are creating a volume based on a snapshot, the volume capacity must be greater than or equal to the capacity of the snapshot.   

