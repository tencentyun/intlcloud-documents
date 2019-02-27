
## API Description
The API CreateAudit is used to create CloudAudit.
Domain name for API access: `cloudaudit.api.qcloud.com`

## Request Parameters
The following request parameter list only provides the API request parameters.

| Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| IsMultiRegionAudit	| No |	Number	| Indicates whether to enable multi-region collection. 0: Disable; 1: Enable. |
| KmsKeyId	| No |	String	| The scretId of Kms, which is used to encrypt data. |
| Name | Yes | String | CloudAudit name, which has a length of 3-128 bytes. Only ASCII coded letters (`a-z, A-Z`), numbers (`0-9`) and underscore (`_`) are allowed. |
| CosBucketName	| Yes |	String	| The name of the receiving COS Bucket. Refer to the naming requirements for COS. |
| CosKeyPrefix | No | String | COS bucket Prefix. For the naming convention, see COS documentation. |
| CmqTopicName	| No |	String	| CMQ topic name, which is required if CMQ is enabled. Refer to the naming requirements for CMQ. |
> **Note:**
> Each user can create up to 50 CloudAudits.


## Response Parameters


| Parameter Name | Type | Description |
|---------|---------|---------|
| IsMultiRegionAudit | Number | Indicates whether to enable multi-region collection. 1: Yes; 0: No. |
| KmsKeyId | String | Kms key ID |
| Name | String | CloudAudit name |
| CosBucketName | String | COS bucket name |
| CosKeyPrefix | String | COS bucket Prefix |
| CmqTopicName | String | CMQ topic name |

## Example
### Request

```
{
   "IsMultiRegionAudit": Number,
   "KmsKeyId": "String",
   "Name": "String",
   "CosBucketName": "String",
   "CosKeyPrefix": "String",
   "CosTopicName": "String"
}
```
### Response

```
{
   "IsMultiRegionAudit": Number,
   "KmsKeyId": "String",
   "Name": "String",
   "CosBucketName": "String",
   "CosKeyPrefix": "String",
   "CmqTopicName": "String"
}
```

