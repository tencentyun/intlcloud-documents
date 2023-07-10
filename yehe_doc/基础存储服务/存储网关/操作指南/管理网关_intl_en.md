After logging in to the console, select the "Gateway" tab. On this page, you can view all the gateways.


## Viewing Gateway Information
Click a "Gateway ID" in the list to enter the gateway details page where you can view the gateway details, rename the gateway, and modify the time zone.

## Editing Gateway Information
On the gateway details page, you can rename the gateway and modify the time zone.

## Managing Network Bandwidth
Generally, you need to allocate network bandwidth resources. This setting can limit the upload and download speeds of gateways and help you make better use of network bandwidth.
On the gateway details page, find the network limit option and click **Edit** to enter the editing page. Upload and download speeds can be limited to between 50 Kbps and 10 Gbps.

## Managing Local Disks (for Universal Gateways Only)
If you use a universal gateway, you can use local disks, DAS storage, or SAN storage as the gateway's upload buffer, cache, and metadata storage. After clicking **Edit**, you can configure the disks mounted to your local gateway VM as "upload buffer", "cache", or "metadata storage".
>In order to guarantee gateway performance, local disks below 10 GB will not appear in the list.
>

**Volume and tape gateways**

- If **the ratio of cache to upload buffer is < 3:2**, the system will not work properly. At this point, you need to increase the cache space.
- If **the ratio of cache to upload buffer is >= 3:2**, the system will automatically adjust the actual usage ratio to 3:2. Therefore, if the ratio is greater than 3:2, there will be idle cache space. At this point, you can increase the upload buffer space to take advantage of the idle cache space.

**File gateway**

- Cache: it is used to store the data to be uploaded and frequently accessed hot data. The recommended space for the upload part is 120% of the amount of data written per day by the business. For example, if the daily written data is 300 GB, the minimum space should be 360 GB. The cache space reserved for hot data can be any value. If you want to improve the performance of data read, you are recommended to reserve as much space as possible. 
>The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.

- Metadata: it is used to store metadata of files so that you can locally query and search for file information faster. Each 1 GB of storage capacity can store the metadata of 100,000 files, and 512 MB of capacity in each metadata disk is reserved for the system. You are recommended to configure the metadata disk capacity based on 1.2 times the number of files expected in the file system. Please evaluate the number of business files and select the appropriate storage capacity. 
>
>- After the metadata disk is full, the files cannot be accessed properly. If the storage utilization reaches 90%, please increase disk capacity in time.
>- New local disk configuration will take effect after the gateway is restarted.

## VTL Device (for Tape Gateway Only)
On the details page of a tape gateway, there is also a list of VTL devices. You can view the VTL's media converter and names of drive targets (which can be discovered by the iSCSI program on the client), where the media converter and drive type are the ones configured when the tape gateway is created.


On this page, you can also set CHAP for each target. Click **Set CHAP** to modify it in the pop-up window.

Note: CHAP information is primarily used for authentication when a volume is connected to through iSCSI. If CHAP authentication is off, any Initiator can connect to the volume. If CHAP is on, the volume can only be accessed by the specified Initiator after being authenticated. CSG uses two-way CHAP, which means that the Initiator and the Target will authenticate each other.

* Initiator Name: enter the name (1–255 lowercase letters or numbers) of the Initiator that is allowed to connect.
* Initiator Key: the password used to authenticate the iSCSI initiator.
* Target Key: the password used to authenticate the iSCSI target (two-way authentication).
>The Target key cannot be the same as the Initiator key.


## Stopping Gateway
If you need to stop a gateway, you can click **Stop** in the "Operation" column in the gateway list. Or, if you need to stop gateways in batches, select the ones you want to stop and click **Stop Gateways** in the **More** drop-down list at the top of the gateway list. Click **Stop Now** in the pop-up window to stop the gateways.


## Starting Gateway
If a gateway is in stopped/configuring state, you can click **Start** in the gateway list to start it.


## Deleting Gateway
If you need to delete a gateway, you can click **Delete** in the "Operation" column in the gateway list. Or, if you need to delete gateways in batches, select the ones you want to stop and click **Delete Gateways** in the **More** drop-down list at the top of the gateway list. Click **Delete Now** in the pop-up window to delete the gateways.
>When a gateway is deleted, the volumes mounted to it will be deleted too.

