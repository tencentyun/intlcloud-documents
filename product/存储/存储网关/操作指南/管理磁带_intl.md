After logging in to the console, select the "Tape" tab. On this page, you can see all the tapes and their states.
![](https://mc.qcloudimg.com/static/img/684795fdc2ca3de6dff602e3fdd559cb/image.png)

## Archiving a Tape
After data is written to a tape using an external application such as a backup program, the tape needs to be archived by an external program. If you use Symantec NetBuckup for backup, you can click [here](https://cloud.tencent.com/document/product/581/12508) to view help information. For other external programs, see their corresponding user manuals.

## Retrieving a Tape
A tape in "archived" state can be retrieved. Click the **Retrieve** button.

* Select gateway: Select the tape gateway to which you need to retrieve the tape. Note: It can be different from the gateway selected at the time of creation.
* Retrieving time: Set the time it takes for the tape to be retrieved (1-5 minutes, 3-5 hours or 5-12 hours). Different retrieving time values have different prices. (At present, only retrieving in 1-5 minutes is supported)

After the tape is retrieved, its state will become "normal" and the data in it can be read by an application such as a backup program.

![](https://mc.qcloudimg.com/static/img/81d97b871a6a0064f366442853000cab/image.png)

## Deleting a Tape
Depending on the needs of your business, you may want to migrate data. In this case, you need to delete the tape. After the tape is deleted, the data in it will be permanently purged, so please be sure to back up the data before deleting the tape.

Click the **Delete** button and then click **OK** in the pop-up to delete the tape. Note: A tape in read/write state cannot be deleted, and if you click "Delete", an error will be displayed.

![](https://mc.qcloudimg.com/static/img/006dd2089d3aefb6b4f1da402ba9136c/image.png)




