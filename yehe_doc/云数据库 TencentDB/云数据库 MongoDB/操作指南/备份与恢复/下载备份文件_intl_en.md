## Getting Backup Download Link
>?To download backups via a sub-account, please grant the sub-account sufficient permissions. For more information, please see [Sub-Account Authorization for Backup Download](https://intl.cloud.tencent.com/document/product/240/36356).

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
1. [Log in to the Linux CVM instance](https://intl.cloud.tencent.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8) and specify an empty download directory. If there is no empty directory, run the following command to create one:
```
mkdir dump
```
>!The private network address of the Linux CVM instance must be within one of the following IP ranges; otherwise, backup files cannot be downloaded.
>- 192.168.0.0/16 
>- 172.16.0.0/16
>- 172.20.0.0/16
>- 172.24.0.0/16
>- 172.27.0.0/16
>- 10.0.0.0/8

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

