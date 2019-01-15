
## SDK Description
  DescribeAudits is used to obtain the CloudAudit information.
## Request Parameters

| Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| auditNameList | Yes | Array | The auditName list |
## Response Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| auditLists | Array | The list of tracking sets |

The parameter auditList is composed of as follows:

| Parameter Name | Type | Description |
|---------|---------|---------|
| IsMultiRegionAudit | Number | Indicates whether to enable multi-region query. 0: No; 1: Yes. |
| KmsKeyId | String | ID of Kms key |
| Name | String | Audit name |
| CosBucketName | String | COS bucket name |
| CosKeyPrefix | String | Prefix of COS bucket |
| CmqTopicName | String | CMQ topic name |
| Status | Number | Audit status. 0: Disabled; 1: Enabled. |


## Example
### Request example

```
$config = array('SecretId'       => 'Your secretId',
                'SecretKey'      => 'Your secretKey',
                'RequestMethod'  => 'GET',
                'DefaultRegion'  => 'gz');
$ca = QcloudApi::load(QcloudApi::MODULE_CLOUDAUDIT, $config);
$package = array('auditNameList'=>'["ayisunxxx"]');
$a = $ca->DescribeAudits($package);
if ($a === false) {
    $error = $ca->getError();
    echo "Error code:" . $error->getCode() . ".\n";
    echo "message:" . $error->getMessage() . ".\n";
    echo "ext:" . var_export($error->getExt(), true) . ".\n";
} else {
    var_dump($a);
}
echo "\nRequest :" . $ca->getLastRequest();
echo "\nResponse :" . $ca->getLastResponse();
echo "\n";
```
### Response example

```
{
    "auditList": [
        {
            "Name": "ayisunxxx",
            "CosBucketName": "sundehuixxx",
            "CosKeyPrefix": "91000000009",
            "Status": 1,
            "IsMultiRegionAudit": 1,
            "CmqTopicName": ""
        }
    ]
}
```



