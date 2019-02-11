
## API Description
  DescribeAudits is used to obtain the CloudAudit information.
Domain name for API access: `cloudaudit.api.qcloud.com`


## Request Parameters
| Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| auditNameList | Yes | Array | The auditName list |
## Response Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| auditLists | Array | The list of tracking sets |

The parameter auditList is composed as follows:

| Parameter Name | Type | Description |
|---------|---------|---------|
| IsMultiRegionAudit	|	Number	| Indicates whether to enable multi-region collection. 0: No; 1: Yes. |
| KmsKeyId | String | Kms key ID |
| Name | String | Audit name |
| CosBucketName | String | COS bucket name |
| CosKeyPrefix | String | COS bucket Prefix |
| CmqTopicName | String | CMQ topic name |
| Status | Number | Audit status. 0: Disabled; 1: Enabled. |


## Example
### Request

```
{
   "auditNameList": [ "String" ]
}
```
### Response

```
{
   "auditLists": [
      {
         "IsMultiRegionAudit": Number,
         "KmsKeyId": "String",
         "Name": "String",
         "CosBucketName": "String",
         "CosKeyPrefix": "String",
         "CmqTopicName": "String",
         "Status":0
      }
   ]
}
```

