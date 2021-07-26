### Does COS support file decompression?

File decompression is a data processing solution provided by Tencent Cloud COS based on [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583). For more information, see [File Decompression](https://intl.cloud.tencent.com/document/product/436/35663).

### Does COS file decompression decompress compressed files in second-level directories?

No. However, you can adjust the function logic to implement the feature.

### Does COS support automatic compression upon file upload?

No.

### Does COS support automatic CDN purging?

You can configure automatic CDN purging via [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583). For operation details, see [CDN Cache Purging](https://intl.cloud.tencent.com/document/product/436/37273).

### Can I back up cloud database data to COS?

You can configure the database backup feature via [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583). After you configure backup function rules for the specified bucket, SCF will regularly scan for your database backup files and dump them to the bucket. For operation details, see [Setting Cloud Database Backup](https://intl.cloud.tencent.com/document/product/436/39629).

