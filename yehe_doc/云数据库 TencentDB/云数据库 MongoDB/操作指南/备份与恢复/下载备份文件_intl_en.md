## Getting Backup Download Link

>
1. Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb) and click an instance name in the instance list to enter the instance management page.
2. On the **Backup and Rollback** > **Backup List** page, click **Download** to get the region code, bucket, and download link that are required for backup download.
![](https://main.qcloudimg.com/raw/64aabb71efe9e9b297adf628f7351d87.png)

## Configuring COSCMD
1. Log in to the CAM Console and get the `SecretId` and `SecretKey` on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.
2. Download the [COSCMD tool](https://intl.cloud.tencent.com/document/product/436/10976) that is required for downloading TencentDB for MongoDB backup files.
3. Configure COSCMD as instructed in [Configuring Parameters](https://intl.cloud.tencent.com/document/product/436/10976#.E9.85.8D.E7.BD.AE.E5.8F.82.E6.95.B0).
For example, if the obtained `SecretId` is `IKIDxxxxxxxxxxx20Eb`, `SecretKey` is `TbecxxxxxxxxxxxT4Yw`, region code is `ap-guangzhou`, and bucket is `mognodb-backup-test-1251937`, then the configuration of COSCMD will be as shown below:
```
coscmd config -a IKIDxxxxxxxxxxx20Eb -s TbecxxxxxxxxxxxT4Yw -b mognodb-backup-test-1251937 -r ap-guangzhou
```

## Downloading Backup File
1. Specify an empty download directory; if there is no directory, create one by running the following command:
```
mkdir dump
```
2. Run the download command with the download link obtained from the TencentDB for MongoDB Console. For example, if the download link is `cmongo_backup/cmgo-pfsumk5l_0/snapshot/1544517026`, the command will be as shown below:
```
coscmd  download -r  cmongo_backup/cmgo-pfsumk5l_0/snapshot/1544517026  dump/
```
>
>- A replica set has only one download link.
>- Each shard of a sharded cluster has a download link. Different shards need to be stored in different directories so as to prevent the downloaded data from being overwritten.
>- `-r` must be added to the command for downloading folders.
3. After the download is completed, you can view the downloaded files as shown below:
![](https://main.qcloudimg.com/raw/163d25eee187b4292261518af8dcd1c1.png)

