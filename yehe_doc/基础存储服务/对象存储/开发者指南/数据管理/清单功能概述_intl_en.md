## What Is Inventory?

The inventory feature helps users manage objects in a bucket. It operates periodically as an alternative to the COS synchronous List API. COS can daily or weekly scan a specified object or objects with the same prefix in a bucket based on an inventory job configured, and export and save the inventory report in CSV format to a specified bucket. The report lists the objects stored and their metadata, and records the desired object attributes as configured.

You can use the inventory feature for various purposes, including but not limited to:

- Reviewing and reporting the replication and encryption status of objects.
- Simplifying and accelerating business workflows and big data jobs.

>!
>- You can configure multiple inventory jobs in one bucket. Such jobs do not directly read the object content during their execution; instead, they only scan the attribute information such as object metadata.
>

## Inventory Parameters

After you configure an inventory job for a bucket, COS regularly scans specified objects in the bucket based on your configuration, and exports an inventory report in .csv format. Currently, the inventory report can record the following information:

| Inventory Information | Description |
| ------------------- | ------------------------------------------------------------ |
| AppID | Account ID |
| Bucket | Name of the bucket where the inventory job is performed |
| fileFormat       |  File format  |
| listObjectCount | 	Number of objects to list, which will be used for billing. For more information, see the inventory feature fees in [Management Feature Fees](https://intl.cloud.tencent.com/document/product/436/40098). |
| listStorageSize | Size of listed objects |
|filterObjectCount  |Number of filtered objects|
|filterStorageSize  |  Size of filtered objects|
| Key | Name of an object file in a bucket. When the CSV file format is used, the key name is URL-encoded and must be decoded before you can use it. |
| VersionId | Version ID of an object. After versioning is enabled for a bucket, COS specifies a version ID for the object added to the bucket. If the inventory is for the current version only, this field is not included. |
| IsLatest | Set to True if the latest object version is used. This field is not included if the inventory is only for the current version of objects. |
| IsDeleteMarker | Set to True if the object is a delete marker. This field is not included if the inventory is only for the current version of objects. |
| Size | Object size in bytes |
| LastModifiedDate | The last modified date of the object |
| ETag | Hash value of an object. It displays only modification to the content of an object, rather than to its metadata. The ETag may be or may not be the MD5 checksum of the data of the object, and this depends on how the object is created and encrypted.|
| StorageClass | Storage class of the object. For more information, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) |
| IsMultipartUploaded | Set to True if the object is uploaded in multiple parts. For more information, see [Multipart Upload](https://intl.cloud.tencent.com/document/product/436/14112) |
| Replicationstatus   | Status of source and replica files in object replication. Source file status: `PENDING` (to be replicated), `COMPLETED` (replicated), or `FAILED` (failed). Replica file status: `REPLICA` (replicated with replica file generated). For more information, see [Actions](https://intl.cloud.tencent.com/document/product/436/19923). |
| Tag | Object tag |

## How to Configure Inventory

Before configuring an inventory, you need to understand two concepts:

- Source bucket: The bucket for which you want to enable inventory, containing:
  - Objects listed in the inventory
  - Configuration of the inventory
- Destination bucket: The bucket where to store the inventory report, containing:
  - An inventory list file
  - Manifest files that describe the location of the inventory list file

An inventory can be configured as follows:

<span id="step1"></span>

#### Specify the information of the objects to be analyzed in the source bucket

To inform COS of object information to be analyzed, you need to configure the following information in the source bucket for the inventory:

- Select object versions: List all the versions of the object or list only the current version. If you select to list all the versions of the object, COS adds information about the object in all historical versions to the inventory report. If you select to list only the current version, COS records only the object in the latest version.
- Configure the attributes of the objects to be analyzed: You need to tell COS which information in the object attributes needs to be included in the inventory report. Currently, supported object attributes include account ID, source bucket name, object file name, object version ID, whether the object is of the latest version, whether the object is a deletion flag, object size, object's last modified date, ETag, object's storage class, cross-region replication tag, and whether the object is a part in multipart upload.

<span id="step2"></span>
#### Configure the storage information for the inventory report

You need to tell COS how often to export the inventory report, which bucket to store the report in, and whether the report should be encrypted. The configuration information is as follows:

- Select an export frequency: Daily or weekly. COS will execute the inventory feature at the specified frequency.
- Select an encryption mode: No encryption or SSE-COS. If SSE-COS is selected, COS encrypts the generated inventory report.
- Configure the output location of the inventory: You need to specify the bucket where to store the inventory report.

>! The destination bucket must be in the same region as the source bucket. They can be the same bucket.
>


## How to Use

#### Configuring inventory via the console

Refer to [Enabling Inventory](https://intl.cloud.tencent.com/document/product/436/30624) to learn how to configure the inventory feature in the console.

#### Configuring inventory via APIs

To enable the inventory feature for a specified bucket using APIs, follow the steps below:

1. Create a COS role.
2. Bind permissions to the COS role.
3. Enable inventory.

#### 1. Creating a COS role
Create a COS role. For more information about the API, see [CreateRole](https://intl.cloud.tencent.com/document/product/598/33561).
Here, `roleName` must be `COS_QcsRole`.
`policyDocument` must be:
```
{
	"version": "2.0",
	"statement": [{
		"action": "name/sts:AssumeRole",
		"effect": "allow",
		"principal": {
			"service": "cos.cloud.tencent.com"
		}
	}]
}
```

#### 2. Binding permissions to the COS role
Grant the log role permissions. For more information about the API, see [AttachRolePolicy](https://intl.cloud.tencent.com/document/product/598/33562).
Here, `policyName` is set to `QcloudCOSFullAccess`, `roleName` is the `COS_QcsRole` in step 1, or the `roleID` returned when `roleName` was created.

#### 3. Enabling inventory
Call the API to enable inventory. For more information about the API, see [PUT Bucket inventory](https://www.tencentcloud.com/document/product/436/30625). Note that the destination bucket to store the inventory files should be in the same region as the source bucket.


## Storage Path of the Inventory Report

The inventory report and manifest files are put in the destination bucket. The inventory report is located in the following path:

```shell
destination-prefix/appid/source-bucket/config-ID/
```

Manifest files are located in the following paths in the destination bucket:

```shell
destination-prefix/appid/source-bucket/config-ID/YYYYMMDD/manifest.json
destination-prefix/appid/source-bucket/config-ID/YYYYMMDD/manifest.checksum
```

The meanings of the paths are as follows:

- **destination-prefix**: This is the "destination prefix" set when you configure the inventory, which can be used to group all inventory reports in a public location in the destination bucket.
- **source-bucket**: This is the name of the source bucket corresponding to the inventory report. This folder is added to avoid conflicts that may occur when multiple source buckets send their inventory reports to the same destination bucket.
- **config-ID**: This is the "inventory name" set when you configure the inventory. If multiple inventory reports are configured in the same source bucket and delivered to the same destination bucket, config-ID can be used to distinguish among different reports.
- **YYYYMMDD**: Timestamp, including the time and date when the bucket scan is started when the inventory report is generated.
- **manifest.json**: This is the manifest file.
- **manifest.checksum**: This is the MD5 of the content of the manifest.json file.

There are two manifest files: manifest.json and manifest.checksum.

>?
> The following describes the manifest files:
> - Both manifest.json and manifest.chenksum are manifest files. manifest.json describes the location of the inventory report, and manifest.checksum is the MD5 of the content of the manifest.json file. Each time a new inventory report is delivered, it is accompanied by a new set of manifest files.
> - Each manifest contained in manifest.json provides metadata and basic information about the inventory, including:
> - Source bucket name.
> - Destination bucket name.
> - Inventory version.
> - Timestamp, including the time and date when the bucket scan is started when the inventory report is generated.
> - Format and architecture of the inventory file.
>  - Object key, size, and md5Checksum of the inventory report in the destination bucket.
>   

The following example shows a manifest in the manifest.json file for CSV-formatted inventory:

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

#### Inventory consistency

All of your objects might not appear in each inventory list. The inventory list provides eventual consistency for PUTs of both new objects and overwrites, and DELETEs. Therefore, the inventory report possibly does not include the latest added or deleted object. For example, if the user uploads or deletes an object when COS is executing an inventory job configured by the user, the results of the upload or deletion operations may not be reflected in the inventory report.

If you want to verify the object status before the execution, we recommend you call the [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) API to extract the object metadata, or check the object attributes in the COS console.
