This document describes common elements used in batch operation.

## Manifest

| Node Name | Parent Node | Description | Type | Required |
| -------- | -------- | ------------------------------------------------------------ | --------------- | -------- |
| Location | Manifest | Location of the object inventory | Location Object | Yes |
| Spec  | Manifest | Format of the object inventory. If the inventory is a CSV file, this element will describe fields in the inventory | Spec Object | Yes |

## Location

| Node Name | Parent Node | Description | Type | Required |
| --------------- | -------- | ------------------------------------------------ | ------ | -------- |
| ETag   | Location | Specifies the ETag of the object inventory; length: 1–1,024 bytes | String | Yes |
| ObjectArn | Location | Specifies the unique resource ID of the object inventory; length: 1–1,024 bytes | String | Yes |
| ObjectVersionId | Location | Specifies the version ID of the object inventory; length: 1–1,024 bytes | String | No |

## Spec

| Node Name | Parent Node | Description | Type | Required |
| ------ | ------ | ------------------------------------------------------------ | ---------------- | -------- |
| Fields | Spec | Describes fields in the inventory. If `Format` is `COSBatchOperations_CSV_V1`, this element is required to specify fields in the CSV file. Valid values: `Ignore`, `Bucket`, `Key`, `VersionId` | Array of Strings | No |
| Format | Spec | Specifies the format of the object inventory. Valid values: `COSBatchOperations_CSV_V1`, `COSInventoryReport_CSV_V1` | String | Yes |

## Operation 

>Operation in a single job can only contain one of the following operations.

| Node Name | Parent Node | Description | Type | Required |
| ------------------------ | --------- | -------------------------------------------------- | ------------------------ | -------- |
| COSPutObjectCopy | Operation | Specifies the parameters for batch replication of objects in the inventory | COSPutObjectCopy Object | No |
| COSInitiateRestoreObject | Operation | Specifies the parameters for batch restore of objects in archived storage type in the inventory | COSInitiateRestoreObject | No |

## COSPutObjectCopy

| Node Name | Parent Node | Description | Type | Required |
| ------------------------- | ---------------- | ------------------------------------------------------------ | -------------------------- | -------- |
| AccessControlGrants | COSPutObjectCopy | Controls the access permissions of an object | AccessControlGrants Object | No |
| CannedAccessControlList | COSPutObjectCopy | Defines the ACL attribute of an object. Valid values: `private`, `public-read` | String | No |
| MetadataDirective  | COSPutObjectCopy | Whether to copy the source file metadata. Enumerated values: `Copy`, `Replaced`. Default value: `Copy`. <br><li>If the flag is `Copy`, the source file metadata will be copied. <br><li>If the flag is `Replaced`, the metadata will be modified according to the header information of the request | String  | No |
| ModifiedSinceConstraint | COSPutObjectCopy | If the object is modified after the specified time, the operation will be performed, otherwise `412` will be returned | Timestamp | No |
| UnModifiedSinceConstraint | COSPutObjectCopy |  If the object is not modified after the specified time, the operation will be performed; otherwise `412` will be returned | Timestamp | No |
| NewObjectMetadata  | COSPutObjectCopy | Configures the metadata of an object | NewObjectMetadata Object | No |
| StorageClass  | COSPutObjectCopy | Configures the storage class of an object. Enumerated values: `STANDARD`, `STANDARD_IA`. Default value: `STANDARD`. | String | No |
| TargetResource  | COSPutObjectCopy | Configures the destination bucket for the replication. Please specify it with "qcs", e.g. `qcs::cos:ap-beijing::result-1250000000` | String | Yes |

### COSInitiateRestoreObject

| Node Name | Parent Node | Description | Type | Required |
| ---------------- | ------------------------ | ------------------------------------------------------- | -------------------------- | -------- |
| ExpirationInDays | COSInitiateRestoreObject | Configures the number of days after which the copy will expire and be automatically deleted. The value is an integer between 1 and 365 | AccessControlGrants Object | Yes |
| JobTier | COSInitiateRestoreObject | String | Yes |

## AccessControlGrants

| Node Name | Parent Node | Description | Type | Required |
| -------- | ------------------- | ------------------ | --------------- | -------- |
| COSGrant | AccessControlGrants | Configures access control | COSGrant Object | No |

## COSGrant

| Node Name | Parent Node | Description | Type | Required |
| ---------- | -------- | ---------------------------------------------------------- | -------------- | -------- |
| Grantee | COSGrant | Specifies to whom a permission is granted | Grantee Object | Yes |
| Permission | COSGrant | Specifies the permission to be granted. Enumerated values: `READ`, `WRITE`, `FULL_CONTROL` | String | Yes |

## Grantee

| Node Name | Parent Node | Description | Type | Required |
| -------------- | ------- | ------------------------------------------------------------ | ------ | -------- |
| DisplayName | Grantee | Username | String | No |
| Identifier | Grantee | User ID in qcs format (UIN), e.g. `qcs::cam::uin/100000000001:uin/100000000001` | String | Yes |
| TypeIdentifier | Grantee | Specifies an identifier type. Currently, only user ID is supported. Enumerated value: `ID` | String | Yes |

## NewObjectMetadata

| Node Name | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | --------------------------------------------------- | ---------------------- | -------- |
| CacheControl | NewObjectMetadata | Cache directives as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentDisposition | NewObjectMetadata | File name as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentEncoding | NewObjectMetadata | Encoding format as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentType | NewObjectMetadata | Content type as defined in RFC 2616, which will be stored in the object metadata | String | No |
| HttpExpiresDate | NewObjectMetadata | Cache expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| SSEAlgorithm | NewObjectMetadata | Server-side encryption algorithm. Currently, only AES256 is supported | String | No |
| UserMetadata | NewObjectMetadata | Includes user-defined object metadata | Array of Key and Value | No |

## Report

| Node Name | Parent Node | Description | Type | Required |
| ----------- | ------ | ------------------------------------------------------------ | ------- | -------- |
| Bucket | Report | Bucket to which a job report is delivered | String | Yes |
| Enabled | Report | Specifies whether to output a job report | Boolean | Yes |
| Format | Report | Job report format. Valid value: `Report_CSV_V1` | String | Yes  |
| Prefix | Report | Job report prefix; length: 0–256 bytes | String | No |
| ReportScope | Report | Determines whether to record information on all operations or only failed operations in a job report. Valid values: `AllTasks`, `FailedTasksOnly` | String | Yes |

## ProgressSummary

| Node Name | Parent Node | Description | Type |
| ---------------------- | --------------- | ------------------ | ------- |
| NumberOfTasksFailed | ProgressSummary | Number of failed operations | Integer |
| NumberOfTasksSucceeded | ProgressSummary | Number of successful operations | Integer |
| TotalNumberOfTasks | ProgressSummary | Total number of operations | Integer |
