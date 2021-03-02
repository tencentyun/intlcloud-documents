## What Is Inventory

Inventory is a feature that helps users manage bucket objects. It operates periodically and as an alternative to the COS synchronous List API operation. COS can daily or weekly scan a specified object or objects with a same prefix in a bucket based on an inventory task configured by the user, and export and store an inventory report as a CSV file in the bucket specified by the user. The file lists stored objects and corresponding metadata, and records the desired object attribute information based on the configuration.

You can use the inventory feature for various purposes, including but not limited to:

- Review and report replication and encryption states of an object.
- Streamline and speed up service workflows and big data jobs.

> !You can configure multiple inventory tasks for one bucket. COS doesn’t directly read the content of an object, but only scan the attribute information such as metadata of the object.

## Inventory Parameters

After you configures an inventory task for a bucket, COS regularly scans a specified object in the bucket based on your configuration, and exports an inventory report in .csv format. Currently, the inventory report can record the following information:

| Inventory Information | Description |
| ------------------- | ------------------------------------------------------------ |
| AppID               | Account ID                                                |
| Bucket | Name of the bucket for which an inventory task is executed. |
| fileFormat       |  File format  |
| listObjectCount | Number of listed objects | 
| listStorageSize | Size of listed objects | 
|filterObjectCount  |Number of filtered objects|
|filterStorageSize  |  Size of filtered objects|
| Key | Name of an object file in a bucket. When using the CSV file format, the key name is URL-encoded and must be decoded before you can use it. |
| VersionId | Version ID of an object. After version control is enabled for a bucket, COS specifies a version ID for the object added to the bucket. If the list is for the current version only, the inventory does not include this field. |
| IsLatest | Sets to True if the latest object version is used. This field is not included if the list is only for the current version of objects. |
| IsDeleteMarker | Sets to True if the object is a delete marker. This field is not included if the list is only for the current version of objects. |
| Size | Size of an object (in bytes) |
| LastModifiedDate | Last modified date of an object (the most recent date prevails) |
| ETag | Hash value of an object. It displays only modification to the content of an object, rather than to its metadata. The ETag may be or may not be the MD5 checksum of the data of the object, and this depends on how the object is created and encrypted.|
| StorageClass | Storage class of the object. For more information, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) |
| IsMultipartUploaded | Sets to True if the object is uploaded in multiple parts. For more information, see [Multipart Upload](https://intl.cloud.tencent.com/document/product/436/14112) |
| Replicationstatus | Sets to PENDING, COMPLETED, FAILED, or REPLICA. For more information, see [Cross-Region Replication Descriptions](https://intl.cloud.tencent.com/document/product/436/19923).|

## How to Configure the Inventory

Before configuring the inventory, you need to understand two concepts:

- Source bucket: The bucket for which the inventory is to be enabled
  - Objects listed in the inventory
  - Configuration of the inventory
- Destination bucket: The bucket where to store the inventory report, containing
  - An inventory list file
  - Manifest files that describe the location of the inventory list file

An inventory can be configured in the following steps:

<span id="step1"></span>

#### Specify the information of the objects to be analyzed in the source bucket

To inform COS of object information to be analyzed, you need to configure the following information in the source bucket for the inventory:

- Select object versions: List all the versions of the object or list only the current version. If you select to list all the versions of the object, COS adds information about the object in all historical versions to the inventory report. If you select to list only the current version, COS records only the object in the latest version.
- Configure the attributes of the objects to be analyzed: You need to tell COS which information in the object attributes needs to be included in the inventory report. Currently, supported object attributes include account ID, source bucket name, object file name, object version ID, whether the object is of the latest version, whether the object is a deletion flag, object size, object's last modified date, ETag, object's storage class, cross-region replication tag, and whether the object is a part in multipart upload.

<span id="step2"></span>
#### Configure the storage information for the inventory report

You need to inform COS of an export frequency of the inventory report, a bucket used to store the inventory report, and whether the inventory report needs to be encrypted. Please see the configuration details as below:

- Select an export frequency: Daily or weekly. COS will execute the inventory feature at the specified frequency.
- Select an encryption mode: No encryption or SSE-COS. If SSE-COS is selected, COS encrypts the generated inventory report.
- Configure an export location: You need to specify the bucket to store the inventory report.

> !The destination bucket must be in the same region as the source bucket. They can be the same bucket.


## Directions

### Configuring an Inventory in the Console

You can refer to the console document [Enabling Inventory](https://intl.cloud.tencent.com/document/product/436/30624) to learn how to configure the inventory feature in the console.

### Configuring an Inventory Through APIs

You can refer to the following API documents to learn how to configure an inventory through APIs:

- [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) 
- [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) 
- [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) 
- [List Bucket Inventory Configurations](https://intl.cloud.tencent.com/document/product/436/30627) 

## Storage Path for the Inventory Report

The inventory report and related manifest files are published in the destination bucket. The inventory report is published in the following path:

```shell
destination-prefix/appid/source-bucket/config-ID/
```

Manifest-related files are located in the following path in the destination bucket:

```shell
destination-prefix/appid/source-bucket/config-ID/YYYYMMDD/manifest.json
destination-prefix/appid/source-bucket/config-ID/YYYYMMDD/manifest.checksum
```

Meaning of the path is as follows:

- **desitination-prefix**: "Destination Prefix" set by the user during configuration of the inventory. It may be used to group all inventory reports in a public location in the destination bucket.
- **source-bucket**: Name of the source bucket corresponding to the inventory report. This folder is intended to prevent possible conflicts when inventory reports from multiple source buckets are sent to a same destination bucket.
- **config-ID**: "Inventory Name" set by the user during configuration of the inventory. When multiple inventory reports are set for a same source bucket and sent to a same destination bucket, you can specify config-ID to distinguish between the different inventory reports.
- **YYYY-MM-DD-HH-MM**: Timestamp, including the time and the date when the bucket starts to be scanned during generation of the inventory report.
- **manifest.json**: Manifest file.
- **manifest.checksum**: MD5 of the content of the manifest.json file.

The related manifest files include two files: manifest.json and manifest.checksum.

> The following describes the related manifest files:
> - Both manifest.json and manifest.checksum are manifest files. manifest.json describes the location of the inventory report, and manifest.checksum is the MD5 of manifest.json. Each newly delivered inventory report comes with a set of new manifest files.
> - Each manifest included in manifest.json provides metadata and other basic information related to the inventory. The information includes:
>   - Name of the source bucket
>   - Name of the destination bucket
>   - Inventory version
>   - Timestamp, including the date and the time when the bucket starts to be scanned during generation of the inventory report.
>   - Format and architecture of the inventory file
>  - Object key, size, and md5Checksum of the inventory report in the destination bucket.

The following shows an example of the manifest content in the manifest.json file in .csv format:

```
{
 "sourceAppid": "1250000000",
 "sourceBucket": "example-source-bucket",
 "destinationAppid": "1250000000",
 "destinationBucket": "example-inventory-destination-bucket",
 "fileFormat": "CSV",
 "listObjectCount": "13",
 "listStorageSize": "7212835",
 "filterObjectCount": "13",
 "filterStorageSize": "7212835",
 "fileSchema": "Appid, Bucket, Key, Size, LastModifiedDate, ETag, StorageClass, IsMultipartUploaded, ReplicationStatus",
 "files": [
  {
   "key": "cos_bucket_inventory/1250000000/examplebucket/inventory01/04d73d9debc73d9f0bf85af461abde6c.csv.gz",
   "size": "502",
   "md5Checksum": "7d40288a09c25b302ad6cb5fced54f35"
  }
 ]
}
```

### Inventory Consistency

All of your objects might not appear in each inventory list. The inventory list provides eventual consistency for PUTs of both new objects and overwrites, and DELETEs. Therefore, the inventory report possibly does not include the latest added or deleted object. For example, if the user uploads or deletes an object when COS is executing an inventory task configured by the user, the results of the upload or deletion operations may not be reflected in the inventory report.

To validate the status of the object before COS performs an operation, you can search for the metadata of the object by using the [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) API, or check the attributes of the object in COS Console.
