After logging in to the console, select the "Volume" tab. On this page, you can view all the volumes.

## Viewing Volume Information
Click a "Volume ID" in the list to enter the volume details page where you can view the volume and CHAP authentication details.


## Managing CHAP Authentication
CHAP information is primarily used for authentication when a volume is connected to through iSCSI. If CHAP authentication is off, any Initiator can connect to the volume. If CHAP is on, the volume can only be accessed by the specified Initiator after being authenticated. CSG uses two-way CHAP, which means that the Initiator and the Target will authenticate each other.

On the volume details page, find the CHAP authentication configuration. After clicking **Edit**, you can set the authentication information, including:

* Initiator Name: enter the name (1–255 lowercase letters or numbers) of the Initiator that is allowed to connect.
* Initiator Key: the password used to authenticate the iSCSI initiator.
* Target Key: the password used to authenticate the iSCSI target (two-way authentication).
>The Target key cannot be the same as the Initiator key.  


## Creating Snapshot
Find the volume in the volume list for which to create a snapshot, click **Create Snapshot** in the "Operation" column, and enter corresponding information in the pop-up window.

* Snapshot name: enter up to 64 letters, numbers, "_", or "-".
* Snapshot description: you can enter optional remarks for the snapshot/

## Migrating Volume (for Disaster Recovery)
Volume supports migration. When the server where a gateway resides fails or the network is exceptional, you can migrate the volumes that cannot be used properly due to the failures or exceptions to a healthy gateway for quick service restoration.

Enter the volume details page, find the "Associated Gateways" in the "Basic Info" column, and click "Modify". Select the target gateway in the pop-up window (the drop-down list will list the eligible gateways) and set the volume name (which cannot be identical with that of any existing volume in the target gateway).

>If the source gateway is already in exceptional state (local volume state cannot be displayed properly due to gateway exceptions), you need to reconnect the migrated new volume after disconnecting the original volume locally.


## Deleting Volume
As needed by your business, you may want to migrate data. In this case, you need to delete the volume. Please make sure that you have stopped writing data to the volume and are not creating a snapshot for it before deleting it.

Find the volume you want to delete in the volume list and click **Delete** in the "Operation" column. Or, if you need to batch delete volumes, select the ones you want to delete and click **Delete** at the top of the list.




