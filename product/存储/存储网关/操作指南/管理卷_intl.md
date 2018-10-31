After logging in to the console, select the "Volume" tab. On this page, you can see all the volumes.

## Viewing Volume Information
Click a "Volume ID" in the list to enter the volume details page where you can view the volume and CHAP authentication details.
![](https://mc.qcloudimg.com/static/img/b0a6717aa638ed6938161f339e835d13/image.png)

![](https://mc.qcloudimg.com/static/img/13aa284cff43b4d4b23cea68281303ba/image.png)


## Managing CHAP Authentication
CHAP information is primarily used for authentication when connecting to a volume using iSCSI. If CHAP is off, any Initiator can connect to the volume. If CHAP authentication is on, the volume can only be accessed by the specified Initiator after being authenticated. CSG uses two-way CHAP, which means that the Initiator and the Target will authenticate each other.

On the volume details page, find the CHAP authentication configuration. After clicking the **Edit** button, you can set the authentication information, including:

* Initiator name: Enter the name (1-255 lowercase letters or digits) of the Initiator that is allowed to connect.
* Initiator key: The password used to authenticate the iSCSI initiator.
* Target key: The password used to authenticate the iSCSI target (two-way authentication).
*Note: The Target key cannot be the same as the Initiator key.

![](https://mc.qcloudimg.com/static/img/207a6b38c396b1267caae0d76ecdf98b/image.png)  


## Creating a Snapshot
Find the volume in the volume list for which to create a snapshot, select the **Create a Snapshot** button in the "Operation" column and enter corresponding information in the pop-up.

* Snapshot name: 64 English letters, Chinese characters, digits, "_" or "-".
* Snapshot description: Optional; you can enter remarks for the snapshot.

![](https://mc.qcloudimg.com/static/img/8ea539bb452a76ffb25ea1cd1ba02287/image.png)

## Migrating a Volume (for Disaster Recovery)
Volume supports migration. When the server where a gateway is located fails or the network is exceptional, you can migrate the volumes that cannot be used properly due to the failures or exceptions to a healthy gateway to quickly restore the service.

Go to the volume details page, find the "Associated gateways" in the "Basic information" column and click "Modify". Select the target gateway in the pop-up (the drop-down box will list the eligible gateways) and set the volume name (which cannot be identical with that of any existing volume in the target gateway).

*Note: If the source gateway is already in exceptional state (local volume state cannot be displayed properly due to gateway exceptions), you need to reconnect the migrated new volume after disconnecting the original volume locally.*


## Deleting a Volume
Depending on the needs of your business, you may want to migrate data. In this case, you need to delete the volume. Please make sure that you have stopped writing data to the volume and are not creating a snapshot for it before deleting it.

Find the volume you want to delete in the volume list and select the **Delete** button in the "Operation" column. Or, if you need to batch delete volumes, select the ones you want to delete and click the **Delete** button at the top of the list.

![](https://mc.qcloudimg.com/static/img/0182179959242eb378a1e70a56a4acb4/image.png)




