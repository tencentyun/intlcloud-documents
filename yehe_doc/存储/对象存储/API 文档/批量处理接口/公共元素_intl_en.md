This document describes common elements used in batch operations.

## Manifest

| Node | Parent Node | Description | Type | Required |
| -------- | -------- | ------------------------------------------------------------ | --------------- | -------- |
| Location | Manifest | Location of the object inventory | Location Object | Yes |
| Spec  | Manifest | Format of the object inventory. If the format is CSV, this element will describe the fields contained in the inventory | Spec Object | Yes |

### Location

| Node | Parent Node | Description | Type | Required |
| --------------- | -------- | -------------------------------------------------- | ------ | -------- |
| ETag | Location | Specifies the ETag of the object inventory; length: 1-1,024 bytes | String | Yes |
| ObjectArn | Location | Specifies the unique resource ID of the object inventory; length: 1-1,024 bytes | String | Yes |
| ObjectVersionId | Location | Specifies the version ID of the object inventory; length: 1-1,024 bytes | String | No |

### Spec

| Node | Parent Node | Description | Type | Required |
| ------ | ------ | ------------------------------------------------------------ | ---------------- | -------- |
| Fields | Spec | Describes the fields contained in the inventory. If the format is `COSBatchOperations_CSV_V1`, this element is required to specify the fields in the CSV file. Valid values: `Ignore`, `Bucket`, `Key`, `VersionId` | Array of Strings | No |
| Format | Spec | Specifies the format of the object inventory. Valid values: `COSBatchOperations_CSV_V1`, `COSInventoryReport_CSV_V1` | String | Yes |

## Operation 

>!A single job can only contain one of the following operations.

| Node | Parent Node | Description | Type | Required |
| ------------------------ | --------- | ------------------------------------------------------ | ------------------------ | -------- |
| COSPutObjectCopy | Operation | Specifies the parameters for the batch replication of objects in the inventory | COSPutObjectCopy Object | No |
| COSInitiateRestoreObject | Operation | Specifies the parameters for the batch restoration of ARCHIVED objects in the inventory | COSInitiateRestoreObject | No |

### COSPutObjectCopy

| Node | Parent Node | Description | Type | Required |
| ------------------------- | ---------------- | ------------------------------------------------------------ | -------------------------- | -------- |
| AccessControlDirective | COSPutObjectCopy | Specifies the ACL replication mode. Valid values: `Copy`, `Replaced`, `Add`.<br/>Copy: inherits the ACL of the source object. <br/>Replaced: replaces the source ACL. <br/>Add: adds a new ACL based on the source ACL. | String | No |
| AccessControlGrants | COSPutObjectCopy | Controls the access permissions of an object | AccessControlGrants Object | No |
| CannedAccessControlList | COSPutObjectCopy | Defines the ACL attribute of an object. Valid values: `private`, `public-read` | String | No |
| PrefixReplace | COSPutObjectCopy | Specifies whether to replace the source object prefix. If set to `true`, the object prefix is replaced. It is used together with `<ResourcesPrefix>` and `<TargetKeyPrefix>`. Default value: `false` | boolean | No |
| ResourcesPrefix | COSPutObjectCopy | Specifies the source object prefix to be replaced. This parameter takes effect only when `<PrefixReplace>` is set to `true`. To replace a directory, the directory should end with a slash (/). This parameter can be up to 1,024 bytes and can be left empty. | string | No |
| TargetKeyPrefix  | COSPutObjectCopy | Specifies the target prefix that replaces the source object prefix. This parameter takes effect only when `<PrefixReplace>` is set to `true`. To replace a directory, the directory should end with a slash (/). This parameter can be up to 1,024 bytes and can be left empty. <br/>Example: Assume that the source object is picture.jpg. If you set `ResourcesPrefix` to `pic` and `TargetKeyPrefix` to `abc`, picture.jpg will be changed to abcture.jpg.<br/>Note:<br/>If `ResourcesPrefix` is empty and `TargetKeyPrefix` carries a value, a prefix will be added.<br/>If both `ResourcesPrefix` and `TargetKeyPrefix` carry a value, the prefix will be replaced.<br/>If `ResourcesPrefix` carries a value and `TargetKeyPrefix` is left empty, the prefix will be deleted.| String | No |
| ModifiedSinceConstraint | COSPutObjectCopy | If the object is modified after the specified time, the operation will be performed; otherwise, 412 will be returned | Timestamp | No |
| UnModifiedSinceConstraint | COSPutObjectCopy | If the object is not modified after the specified time, the operation will be performed; otherwise, `412` will be returned | Timestamp | No |
| MetadataDirective | COSPutObjectCopy | Specifies whether to copy the metadata of the source object, or replace the metadata with that specified in `<NewObjectMetadata>`. Valid values: `Copy`, `Replaced`. `Add`. Copy: inherits the metadata of the source object. Replaced: replaces the source metadata. Add: adds new metadata based on the source metadata. | String | No |
| NewObjectMetadata | COSPutObjectCopy | Configures the metadata of an object | NewObjectMetadata Object | No |
| TaggingDirective | COSPutObjectCopy | Specifies whether to copy the tag of the source object, or replace the tag with that specified in `<NewObjectTagging>`. Valid values: `Copy`, `Replaced`, `Add`. Copy: inherits the tag of the source object. Replaced: replaces the source tag. Add: adds a tag based on the source tag. | String | No |
| NewObjectTagging | COSPutObjectCopy | Configures the object tag. This parameter must be specified if `<TaggingDirective>` is set to `Replace` or `Add`. | NewObjectTagging | No |
| StorageClass  | COSPutObjectCopy | Configures the storage class of an object. Enumerated values: `STANDARD` (default), `STANDARD_IA`. | String | No |
| TargetResource  | COSPutObjectCopy | Configures the destination bucket for the replication. Please specify it with "qcs", e.g., `qcs::cos:ap-beijing::result-1250000000` | String | Yes |

### COSInitiateRestoreObject

| Node | Parent Node | Description | Type | Required |
| ---------------- | ------------------------ | --------------------------------------------------------- | ------- | -------- |
| ExpirationInDays | COSInitiateRestoreObject | Specifies the number of days after which the copy will expire and be deleted automatically. It is an integer ranging from 1 to 365. | Integer | Yes |
| JobTier | COSInitiateRestoreObject | Specifies the restoration mode. Valid values: `Bulk`, `Standard`. | String | Yes |

## AccessControlGrants

| Node | Parent Node | Description | Type | Required |
| -------- | ------------------- | ------------------ | --------------- | -------- |
| COSGrant | AccessControlGrants | Configures access control | COSGrant Object | No |

### COSGrant

| Node | Parent Node | Description | Type | Required |
| ---------- | -------- | ---------------------------------------------------------- | -------------- | -------- |
| Grantee | COSGrant | Specifies the user to which the permission is granted | Grantee Object | Yes |
| Permission | COSGrant | Specifies the permission to be granted. Enumerated values: `READ`, `WRITE`, `FULL_CONTROL` | String | Yes |

#### Grantee

| Node | Parent Node | Description | Type | Required |
| -------------- | ------- | ------------------------------------------------------------ | ------ | -------- |
| DisplayName | Grantee | Username | String | No |
| Identifier | Grantee | User ID in qcs format (UIN), e.g., `qcs::cam::uin/100000000001:uin/100000000001` | String | Yes |
| TypeIdentifier | Grantee | Specifies the identifier type. Currently, only user ID is supported. Enumerated value: `ID` | String | Yes |

## NewObjectMetadata

| Node | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ----------------------------------------------------- | ---------------------- | -------- |
| CacheControl | NewObjectMetadata | Cache directives as defined in RFC 2616. It will be stored as object metadata. | String | No |
| ContentDisposition | NewObjectMetadata | Filename as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentEncoding | NewObjectMetadata | Encoding format as defined in RFC 2616. It will be stored as object metadata. | String | No |
| ContentType | NewObjectMetadata | Content type as defined in RFC 2616. It will be stored as object metadata. | String | No |
| HttpExpiresDate | NewObjectMetadata | Cache expiration time as defined in RFC 2616. It will be stored as object metadata. | String | No |
| SSEAlgorithm | NewObjectMetadata | Server-side encryption algorithm. Currently, only AES256 is supported | String | No |
| UserMetadata | NewObjectMetadata | Includes user-defined object metadata | Array of Key and Value | No |

## Report

| Node | Parent Node | Description | Type | Required |
| ----------- | ------ | ------------------------------------------------------------ | ------- | -------- |
| Bucket | Report | Bucket to which a job report is delivered | String | Yes |
| Enabled | Report | Specifies whether to output a job report | Boolean | Yes |
| Format | Report | Job report format. Valid value: `Report_CSV_V1` | String | Yes  |
| Prefix | Report | Job report prefix; length: 0-256 bytes | String | No |
| ReportScope | Report | Specifies whether the job report records all operations or only failed operations. Valid values: `AllTasks`, `FailedTasksOnly` | String | Yes |

## ProgressSummary

| Node | Parent Node | Description | Type |
| ---------------------- | --------------- | ------------------ | ------- |
| NumberOfTasksFailed | ProgressSummary | Number of failed operations | Integer |
| NumberOfTasksSucceeded | ProgressSummary | Number of successful operations | Integer |
| TotalNumberOfTasks | ProgressSummary | Total number of operations | Integer |
