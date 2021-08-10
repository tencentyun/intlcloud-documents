### What should I do when COSCMD is unavailable?

Please check whether the following requirements are met:
1. The OS is Windows, Linux, or macOS.
2. Local characters use UTF-8 encoding. Otherwise, exceptions will occur when you operate on Chinese files.
3. The local time is in sync with UTC. If there is a large deviation between the two, COSCMD might not function properly.

For more information, please see [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).

### Does COSCMD support regular expressions?

No.

### I can successfully create a bucket with a name containing uppercase letters using COSCMD, but when I perform other operations with a bucket name containing uppercase letters, an error occurs. What is the reason for this?

COSCMD automatically converts uppercase letters to lowercase ones. A bucket name can only contain lowercase letters, numbers, and hyphens (-), with a length not greater than 50 characters. For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

### Can the files in a sub-directory be excluded when I upload or download the files in the root directory with COSCMD?

Yes. You need to use the `--ignore /folder/*` parameter.
For example, if you want to exclude a folder during download, use `coscmd download --ignore /folder/*` to filter out the files in the folder. If you want to ignore files with a certain suffix in the folder, be sure to append `,` to the "*" character, or enclose it with `""`.

### Does COSCMD support using \* to determine objects with a specified prefix to download?

No. You need to use the following command format for download:
```plaintext
coscmd download prefix/ localpath/ -r
```


### How do I use COSCMD to access multiple buckets?

You can use the `-b` and `-r` parameters to specify multiple buckets, for example, `coscmd -b examplebucket-1250000000 examplebucket-1250000001 -r ap-beijing`. Alternatively, you can use the `-c` parameter to specify the configuration file `cos.conf` and configure multiple buckets in the `cos.conf` file.

### Can I use the `list` command to list files by file upload time in COSCMD?

No. You can list files by specifying a prefix. For more information, please see [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).

### Can I use COSCMD to manage buckets of different accounts at the same time?

You can configure only the bucket under one account in the `cos.conf` configuration file. If you need to manage a bucket under another account, switch to the bucket first by using the following command:
```
coscmd config -a SecretID -s SecretKey -b BucketName-APPID -r region
```
`SecretID` and `SecretKey` can be obtained in the [CAM console](https://console.cloud.tencent.com/cam/capi). `BucketName-APPID` indicates the bucket name, and `region` indicates the region where the bucket resides.

### Can I specify multiple buckets in the COSCMD configuration file?

You can configure only one bucket in the COSCMD configuration file. If you need to manage another bucket, specify the bucket name and region in the COSCMD command for bucket switching. 

- Use the `-b <bucketname-appid>` parameter to specify the bucket name, which must be formatted as `BucketName-APPID`.
- Use the `-r <region>` parameter to specify the region where the bucket resides.

### Does COSCMD verify filename duplication for uploaded files?

No. If you upload a file with a duplicate name as an existing file, COSCMD will overwrite the existing file.

### How do I transfer a large number of files with a quicker speed?

Configure an appropriate value for `MAX_THREAD`, which defaults to 5. The number of threads depends on the server performance, and generally, setting its value to 30 can easily take up full bandwidth. For example, you can set the number of concurrent threads to 30 by running the following command:

```
coscmd config -m 30
```

### Does COSCMD verify the content of uploaded files?

No. COSCMD adopts the overwrite upload mode by default. If you need to skip existing identical files, add the `-rs` parameter.

### How do I skip existing identical files when uploading files with COSCMD?

When you upload files with COSCMD, you can add the `-rs` parameter to skip existing files with the same MD5 value. For more information, please see **the methods for uploading files or folders** in [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).

### How do I skip identical files when downloading files with COSCMD?

When downloading a folder, you can use the `-s` or `--sync` parameter to skip identical files that already exist locally (provided that the downloaded files were uploaded via the COSCMD `upload` API and the `x- cos-meta-md5` header was included). An example of the complete command is as follows: `coscmd download -rs  --skipmd5 cos_path local_path`.

### Can I upload multiple folders at the same time with COSCMD?

No. You can upload only one folder at a time. You can put multiple folders that need to be uploaded into a single folder for uploading, but it takes time to copy files locally.

