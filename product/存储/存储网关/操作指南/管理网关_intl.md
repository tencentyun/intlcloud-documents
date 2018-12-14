After logging in to the console, select the "Gateway" tab. On this page, you can see all the gateways.
![](https://mc.qcloudimg.com/static/img/d487be233e18b20b9fea413510408718/image.png)

## Viewing Gateway Information
Click a "Gateway ID" in the list to enter the gateway details page where you can view the gateway details and modify the gateway name and time zone.
![](https://mc.qcloudimg.com/static/img/011d3d7cacc7fb6b1770355d0e31bee9/image.png)
![](https://mc.qcloudimg.com/static/img/c86a717862f4598324826bc18660ff72/image.png)

## Editing Gateway Information
On the gateway details page, you can modify the gateway name and time zone.
![](https://mc.qcloudimg.com/static/img/79ab65c3f032928167938ed4ae0b1efb/image.png)
![](https://mc.qcloudimg.com/static/img/26d3f0a8fee26a0b27c22181c3efd776/image.png)

## Managing Network Bandwidth
Generally, you need to allocate network bandwidth resources. This setting can limit the upload and download speeds of gateways and help you make better use of network bandwidth.
On the gateway details page, find the network restriction option and click the **Edit** button to enter the editing page. Upload and download speeds can be limited to between 50 Kbps and 10 Gbps.
![](https://mc.qcloudimg.com/static/img/7d1280ca7bf72d0e871c3d8972811c9f/image.png)

## Managing Local Disks (for Universal Gateways Only)
If you use a universal gateway, you can use local disks, DAS storage or SAN storage as the gateway's upload buffer, cache and metadata storage. After clicking the **Edit** button, you can configure the disks mounted to your local gateway VM as "upload buffer", "cache" or "metadata storage".
*Note: In order to guarantee gateway performance, local disks below 10 GB will not appear in the list.*
![](https://mc.qcloudimg.com/static/img/7cf2f39c76e02432574c36aa8a644472/image.png)

**Volume and Tape Gateways**

- If **cache:upload buffer < 3:2**, the system will not work properly. At this point, you need to increase the cache space.
- If **cache:upload buffer >= 3:2**, the system will automatically adjust the actual usage ratio of the two parts to 3:2. Therefore, if the ratio is greater than 3:2, there will be idle cache space. At this point, you can increase the upload buffer space to take advantage of the idle cache space.

**File Gateway**

- Cache: Used to store the data to be uploaded and frequently accessed hot data. The recommended space for the upload part is 120% of the amount of data written per day of the business. For example, if the daily written data is 300 GB, the minimum space should be 360 GB. The cache space reserved for hot data can be any value. If you want to improve the performance of data read, it is recommended to reserve as much space as possible. *Note: The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.*

- Metadata: Used to store metadata information of files so that you can locally query and search for file information faster. Each 1 GB storage space can store the metadata information of 100,000 files, and 512 MB of space in each metadata disk is reserved for the system. It is recommended to configure the metadata disk space based on 1.2 times the number of files expected in the file system. Please evaluate the number of business files and select the appropriate storage capacity. *Note: After the metadata disk is full, the files cannot be accessed properly. If the storage usage reaches 90%, please increase disk capacity in time.*

Note: New local disk configuration will take effect after the gateway is restarted. 

## VTL Device (for Tape Gateway Only)
On the details page of a tape gateway, there is also a list of VTL devices. You can view the VTL's media converter and names of drive targets (which can be discovered by the iSCSI program on the client), where the media converter and drive type are configured when creating the tape gateway.
![](https://mc.qcloudimg.com/static/img/2b70d455091b26d10128faa2514c54ad/image.png)

On this page, you can also set CHAP for each target. Click **Set CHAP** to modify it in the pop-up.

Note: CHAP information is primarily used for authentication when connecting to a volume using iSCSI. If CHAP is off, any Initiator can connect to the volume. If CHAP authentication is on, the volume can only be accessed by the specified Initiator after being authenticated. CSG uses two-way CHAP, which means that the Initiator and the Target will authenticate each other.

* Initiator name: Enter the name (1-255 lowercase letters or digits) of the Initiator that is allowed to connect.
* Initiator key: The password used to authenticate the iSCSI initiator.
* Target key: The password used to authenticate the iSCSI target (two-way authentication).
*Note: The Target key cannot be the same as the Initiator key.*

![](https://mc.qcloudimg.com/static/img/e8afd6270a7b4b55fe18f9132a374e06/image.png)


## Stopping a Gateway
If you need to stop a gateway, you can use the **Stop** button in the "Operation" column in the gateway list. Or, if you need to batch stop gateways, select the gateways you want to stop and choose **Stop Gateways** in the **More operations** drop-down menu at the top of the list. Click the **Stop Now** button in the pop-up to stop the gateway.
![](https://mc.qcloudimg.com/static/img/59002464250633bb56f87ccbb1ed52d6/image.png)

## Starting a Gateway
If a gateway is in stopped/configuring state, you can click the **Start** button in the gateway list to start it.


## Deleting a Gateway
If you need to delete a gateway, you can find the **Delete** button in the "Operation" column in the gateway list. Or, if you need to batch delete gateways, select the ones you want to delete and choose **Stop Gateways** in the **More operations** drop-down menu at the top of the list. Click the **Delete Now** button in the pop-up to delete the gateway.
**Note: When the gateway is deleted, the volumes mounted to it will be deleted too.**
![](https://mc.qcloudimg.com/static/img/ae69ba3401d67291ba3b34040362a6dc/image.png)









