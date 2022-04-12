This document describes how to download backup files in the TencentDB for PostgreSQL console.

## Notes
- Both private and public addresses are valid for 15 minutes. Please refresh the page to get new ones upon expiration.
- URL must be enclosed with quotation marks when wget is used to download.

## Directions
### Data backup download
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/pgsql). In the instance list, select a region and click an instance ID to enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** and click **Backup List**.
![](https://qcloudimg.tencent-cloud.cn/raw/25a170dc36f74ac1a00ec3e8f422fa8e.png)
3. Select the backup you want to download from the backup list and click **Download** in its **Operation** column.
4. In the download window, two download addresses are provided: VPC private address and public address.
>?We recommend you copy the download address, [log in to a Linux CVM instance in the same VPC as the TencentDB instance](https://intl.cloud.tencent.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8), and run the `wget` command for download over the private network at a higher speed.
>
![](https://qcloudimg.tencent-cloud.cn/raw/0af2893a802f8c4ce291ac05d9f45a98.png)

### Log backup download
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/pgsql). In the instance list, select a region and click an instance ID to enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** and click **Log Backup List**.
![](https://qcloudimg.tencent-cloud.cn/raw/a07f4c7f9a53b837f8dc8ecad117d1f2.png)
3. Select the backup you want to download from the log backup list and click **Download** in its **Operation** column.
4. In the download window, both VPC private address and public address are provided for download.
![](https://qcloudimg.tencent-cloud.cn/raw/0af2893a802f8c4ce291ac05d9f45a98.png)
