
## Getting a Backup Download Link
>If you need to use the backup download feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>
1. Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb) and click an instance name in the instance list to enter the instance management page.
2. On the **Backup and Rollback** > **Backup List** page, click **Download** to get the region code, bucket, and download link that are required for backup download.
![](https://main.qcloudimg.com/raw/089e0555ba190942b796f1f96e65dd93.png)

## Configuring COSCMD
1. Log in to the CAM Console and obtain the SecretId and SecretKey on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.
2. Download the [COSCMD tool](http://intl.cloud.tencent.com/document/product/436/10976) that is required for downloading TencentDB for MongoDB backup files.
3. Configure COSCMD as instructed in [Configuring Parameters](http://intl.cloud.tencent.com/document/product/436/10976#configuring-parameters).
For example, if the obtained SecretId is `IKIDqbHPVTi5hO2a2KbwhRTPDrM3iv20Eb`, SecretKey is `TbecR6c0W4mKwxw342qV1Rhr2oT4Yw`, region code is `ap-guangzhou`, and bucket is `mognodb-backup-test-1251937`, then the configuration of COSCMD will be as shown below:
```
coscmd config -a IKIDqbHPVTi5hO2a2KbwhRTPDrM3iv20Eb -s TbecR6c0W4mKwxw342qV1Rhr2oT4Yw -b mognodb-backup-test-1251937 -r ap-guangzhou
```

## Downloading a Backup File
1. Specify an empty download directory; if there is no directory, create one by running the following command:
```
mkdir dump
```
2. Run the download command with the download link obtained from the TencentDB for MongoDB Console. For example, if the download link is `cmongo_backup/cmgo-pfsumk5l_0/snapshot/1544517026`, the command will be as shown below:
```
coscmd  download -r  cmongo_backup/cmgo-pfsumk5l_0/snapshot/1544517026  dump/
```
>- A replica set has only one download link.
>- Each shard of a sharding cluster has a download link. Different shards need to be stored in different directories so as to prevent the downloaded data from being overwritten.
>- The `-r` must be added to the command for downloading folders.
3. After the download is completed, you can view the downloaded files as shown below:
![](https://main.qcloudimg.com/raw/163d25eee187b4292261518af8dcd1c1.png)

