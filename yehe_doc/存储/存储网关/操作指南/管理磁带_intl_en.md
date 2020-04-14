After logging in to the console, select the "Tape" tab. On this page, you can view all the tapes and their states.

## Archiving Tape
After data is written to a tape by using an external application such as a backup program, the tape needs to be archived through the external program. If you use Symantec NetBuckup for backup, you can click [here](https://intl.cloud.tencent.com/document/product/581/35689) to view help information. For other external programs, please see their corresponding user manuals.

## Retrieving Tape
A tape in "archived" state can be retrieved. Click **Retrieve**.

* Select Gateway: select the tape gateway to which you need to retrieve the tape. Note: it can be different from the gateway selected at the time of creation.
* Retrieving Time: set the time it takes for the tape to be retrieved (1–5 minutes, 3–5 hours, or 5–12 hours). The price varies by retrieving time. Currently, only the 1–5 minutes option is available.

After the tape is retrieved, its state will become "normal" and the data in it can be read by applications such as a backup program.

## Deleting Tape
As needed by your business, you may want to migrate data. In this case, you need to delete the tape. After the tape is deleted, the data in it will be permanently purged, so please be sure to back up the data before deleting the tape.

Click **Delete** and then click **OK** in the pop-up window to delete the tape.
>A tape that is being read/written cannot be deleted, and if you click "Delete", an error will be displayed.
>




