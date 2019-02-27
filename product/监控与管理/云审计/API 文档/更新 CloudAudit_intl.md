
## API Description
The API UpdateAudit is used to update CloudAudit. It can be used to update certain settings in the specified log file, such as the path and COS Bucket. The name of CloudAudit cannot be modified. You do not need to disable the CloudAudit service when modifying the path. If the COS Bucket to be modified was a target of the CloudAudit log file, it can be modified successfully; otherwise, you need to manually grant CloudAudit the write permission to the COS Bucket.

Domain name for API access: `cloudaudit.api.qcloud.com`


## Request Parameters
The following request parameter list only provides the API request parameters.

| Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| IsMultiRegionAudit	| No |	Number	| Indicates whether to enable multi-region collection. 0: Disable; 1: Enable. |
| KmsKeyId	| No |	String	| The scretId of Kms, which is used to encrypt data. |
| Name	| Yes |	String	| CloudAudit name, which is limited to 3-128 bytes and only contains ASCII characters including letters (`a-z, A-Z`), numbers (`0-9`), and underscores (`_`). |
| CosBucketName	| Yes |	String	| The name of the receiving COS Bucket. Refer to the naming requirements for COS. |
| CosKeyPrefix	| No |	String	| COS Bucket Prefix. Refer to the naming requirements for COS. |
| CmqTopicName	| No |	String	| CMQ topic name, which is required if CMQ is enabled. Refer to the naming requirements for CMQ. |
## Response Parameters

| Parameter Name | Type | Description |
|---------|---------|--------|
| IsMultiRegionAudit	|	Number	| Indicates whether to enable multi-region collection. 0: Disable; 1: Enable. |
| KmsKeyId	|	String	| The scretId of Kms, which is used to encrypt data. |
| Name	|	String	| CloudAudit name, which is limited to 3-128 bytes and only contains ASCII characters including letters (`a-z, A-Z`), numbers (`0-9`), and underscores (`_`). |
| CosBucketName	|	String	| The name of the COS Bucket to be delivered. Refer to the naming requirements for COS. |
| CosKeyPrefix	|	String	| COS Bucket Prefix. Refer to the naming requirements for COS. |
| CmqTopicResource | String | CMQ topic resource |
| CmqTopicName	|	String	| CMQ topic name, which is required if CMQ is enabled. Refer to the naming requirements for CMQ. |

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
   "CmqTopicResource": "String",
   "CmqTopicName": "String",
}
```

