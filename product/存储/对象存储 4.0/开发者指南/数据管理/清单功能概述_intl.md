## What Is Inventory?

Inventory is a feature that helps you manage objects in a bucket and can gradually replace the List API operation in COS. COS can be configured according to your inventory task to regularly scan the specified objects or objects with the same object prefix in your bucket daily or weekly and output an inventory report, which is stored in a specified bucket as a CSV file. The file lists the stored objects and their corresponding metadata and records the object attribute information as desired according to your configuration information.

You can use the inventory feature for various purposes, including but not limited to:

- Reviewing and reporting the replication and encryption status of objects.
- Simplifying and accelerating business workflows and big data jobs.

> - You can configure multiple inventory tasks in one bucket. Such tasks do not directly read the object content during their execution; instead, they only scan the attribute information such as object metadata.
>- Currently, the inventory feature is not available for COS buckets in Finance Cloud regions.

## Inventory Parameters

After you configure an inventory task, COS regularly scans the specified objects in your bucket according to the configuration and outputs an inventory report as a CSV file. Currently, the following information can be recorded in the COS inventory report:

| Inventory information | Description |
| ------------------- | ------------------------------------------------------------ |
| AppID | Account ID |
| Bucket | Name of the bucket where the inventory task is performed |
| Key | Name of the object file in the bucket. If CSV file format is used, the object file name is URL-encoded and must be decoded before it can be used |
| VersionId | Object version ID. If versioning is enabled for the bucket, COS assigns a version number to the objects added to the bucket. Do not include this field if the list is only for the current version of the object |
| IsLatest | Set this field to true if the version of the object is up to date. Do not include this field if the list is only for the current version of the object |
| IsDeleteMarker | Set this field to true if the object is a deletion flag. Do not include this field if the list is only for the current version of the object |
| Size | Object size in bytes |
| LastModifiedDate | The last modified date of the object |
| ETag | An entity tag (ETag) is a hash of the object. It only reflects changes to the object's content but not the object's metadata. It may or may not be an MD5 digest of the object data. This depends on how the object was created and encrypted |
| StorageClass | Storage class used to store the object. For more information, see [Storage Type](https://intl.cloud.tencent.com/document/product/436/13324) |
| IsMultipartUploaded | Set this field to true if the object is uploaded in multiple parts. For more information, see [Multipart Upload Overview](https://intl.cloud.tencent.com/document/product/436/14112) |
| Replicationstatus | Set to PENDING, COMPLETED, FAILED, or REPLICA. |

## How to Configure Inventory

Before configuring an inventory, you need to understand two concepts:

- Source bucket: The bucket for which you want to enable inventory, containing:
  - Objects listed in the inventory
  - Configuration of the inventory
- Destination bucket: The bucket where to store the inventory report, containing

  - An inventory list file
  - Manifest files that describe the location of the inventory list file

An inventory can be configured in the following steps:

1. [Specify the information of the objects to be analyzed in the source bucket](#step1).
2. [Configure the storage information for the inventory report](#step2).
3. [Configure other configuration items](#step3).

<span id="step1"></span>

### Specify the information of the objects to be analyzed in the source bucket

You need to tell COS which objects are to be analyzed. Therefore, when configuring an inventory, you need to configure the following information in the source bucket:

- Select object version: List all object versions or only the current version. If you choose to list all object versions, COS will include all historical versions of your objects of the same name in the inventory report. If you choose to list only the current version, COS will only record your objects of the latest version.
- Configure the attributes of the objects to be analyzed: You need to tell COS which information in the object attributes needs to be included in the inventory report. Currently, supported object attributes include account ID, source bucket name, object file name, object version ID, whether the object is of the latest version, whether the object is a deletion flag, object size, object's last modified date, ETag, object's storage class, cross-region replication tag, and whether the object is a part in multipart upload.


<span id="step2"></span>
### Configure the storage information for the inventory report

You need to tell COS how often to export the inventory report, which bucket to store the report in, and whether the report should be encrypted. The configuration information is as follows:

- Select inventory export frequency: Daily or weekly. You can use this configuration item to tell COS how often the inventory feature should be executed.
- Select inventory encryption: No encryption or SSE-COS. If you choose SSE-COS encryption, the generated inventory report will be encrypted.
- Configure the output location of the inventory: You need to specify the bucket where to store the inventory report.

> The destination bucket must be in the same region as the source bucket. They can be the same bucket.

<span id="step3"></span>
### Configure other configuration items

To ensure that COS can store the inventory report in the destination bucket, you need to add a bucket policy to the destination bucket to allow COS to put the objects in it.
The policy is as follows:

```xml
   {
     "Statement": [
       {
         "Action": [
           "name/cos:PutObject"
         ],
         "Effect": "allow",
         "Principal": {
           "qcs": [
             "qcs::cam::uin/100000000001:service/cdn"
           ]
         },
         "Resource": [
           "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
         ]
       }
     ],
     "version": "2.0"
   }
```

## How to Use

### Configuring an Inventory in the Console

You can refer to the console document [Enabling Inventory](https://intl.cloud.tencent.com/document/product/436/30624) to learn how to configure the inventory feature in the console.

### Configuring an Inventory Through APIs

You can refer to the following API documents to learn how to configure an inventory through APIs:

- [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) 
- [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) 
- [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) 
- [List Bucket Inventory Configurations](https://intl.cloud.tencent.com/document/product/436/30627) 

## Storage Path of the Inventory Report

The inventory report and Manifest-related file are put in the destination bucket. The inventory report is located in the following path:

```shell
destination-prefix/source-bucket/config-ID/data/
```

Manifest-related files are located in the following folder in the destination bucket:

```shell
destination-prefix/source-bucket/config-ID/YYYY-MM-DD-HH-MM/manifest.json
destination-prefix/source-bucket/config-ID/YYYY-MM-DD-HH-MM/manifest.checksum
```

The meanings of the paths are as follows:

- **desitination-prefix**: This is the "destination prefix" set when you configure the inventory, which can be used to group all inventory reports in a public location in the destination bucket.
- **source-bucket**: This is the name of the source bucket corresponding to the inventory report. This folder is added to avoid conflicts that may occur when multiple source buckets send their inventory reports to the same destination bucket.
- **config-ID**: This is the "inventory name" set when you configure the inventory. If multiple inventory reports are configured in the same source bucket and sent to the same destination bucket, config-ID can be used to distinguish among different reports.
- **YYYY-MM-DD-HH-MM**: Timestamp, including the time and date when the bucket scan is started when the inventory report is generated.
- **manifest.json**: This is the Manifest file.
- **manifest.checksum**: This is the MD5 of the content of the manifest.json file.

In summary, there are two Manifest-related files: manifest.json and manifest.checksum.

> Below describes the Mainfest files:
> - Both manifest.json and manifest.chenksum are Manifest files. manifest.json describes the location of the inventory report, while manifest.checksum is the MD5 of the content of the manifest.json file. Each time a new inventory report is delivered, a new pair of Manifest files are carried.
> - Each Manifest contained in manifest.json provides metadata and basic information about the inventory, including:
> - Source bucket name.
> - Destination bucket name.
> - Inventory version.
> - Timestamp, including the time and date when the bucket scan is started when the inventory report is generated.
> - Format and architecture of the inventory file.
> - Object key, size, and MD5 checksum of the inventory report in the destination bucket.

Below is a Manifest example in the manifest.json file of an inventory in CSV format:

```
{
    "sourceBucket": "Example-source-bucket",
    "destinationBucket": "Example-inventory-destination-bucket",
    "version": "2016-11-30",
    "creationTimestamp" : "1514944800000",
    "fileFormat": "CSV",
    "fileSchema": "Bucket, Key, Size, StorageClass, ETag, ReplicationStatus, MultipartUploaded, LastModifiedDate, VersionId, IsLatest, IsDeleteMarker",
    "files": [
        {
            "key": "destination-prefix/Example-source-bucket/config-ID/data/939c6d46-85a9-4ba8-87bd-9db705a579ce.csv.gz",
            "size": 2147483647,
            "MD5checksum": "f11166069f1990abeb9c97ace9cdfabc",
            "inventoriedRecord": 58050695
        }
    ]
}
```

### Inventory Consistency

All of your objects may not appear in each inventory list. The inventory list provides eventual consistency for PUTs of both new objects and overwrites, and DELETEs. For example, if you perform operations such as object upload or deletion when COS is executing an inventory task you configured, the results of such operation may not be reflected in the inventory report.

If you need to verify the status of an object before manipulating it, you are recommended to use the HEAD Object API to retrieve the object metadata or check the object attributes in the COS Console.
